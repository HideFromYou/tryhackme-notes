# TryHackMe - Overpass

## Overview
Completed the Overpass TryHackMe challenge room, focusing on web enumeration, broken authentication exploitation, SSH credential compromise, Linux enumeration, and privilege escalation through cron job hijacking.

This challenge simulated a realistic attack chain from web application weakness to root compromise.

---

## Skills Practiced

- Network reconnaissance
- Web enumeration
- Directory brute forcing
- Authentication bypass
- Cookie manipulation
- SSH key cracking
- Linux enumeration
- Cron job abuse
- Host file manipulation
- Reverse shell deployment
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and application attack surface.

Discovered services included:

- SSH
- HTTP

Web enumeration identified hidden application functionality and administrative interfaces.

This established the attack surface.

---

### Web Enumeration
Application inspection revealed an administrative login portal and downloadable application resources.

Source code and client-side logic analysis exposed weak authentication design.

This revealed the initial exploitation path.

---

### Broken Authentication Exploitation
Authentication controls relied on insecure client-side session validation.

By manually manipulating browser cookies, administrative access was achieved without valid credentials.

Technique:

- browser developer tools
- cookie/session token manipulation
- authentication logic abuse

This exposed sensitive internal data.

---

### Credential Discovery
Administrative access revealed an SSH private key.

The key was passphrase protected and required offline cracking.

This established the next attack phase.

---

### Initial Access
SSH key cracking recovered valid authentication material.

Access was obtained through SSH using compromised credentials.

This established the initial foothold.

---

### Linux Enumeration
Post-exploitation enumeration identified privilege escalation opportunities.

Activities included:

- scheduled task inspection
- file permission analysis
- local service discovery
- writable system file analysis

---

### Privilege Escalation
Privilege escalation was achieved through cron job hijacking.

A privileged scheduled task retrieved and executed a script using hostname resolution.

By manipulating:

```text
/etc/hosts
```

traffic was redirected to attacker-controlled infrastructure, causing the privileged cron job to execute malicious code.

This resulted in root shell access.

---

## Tools Used

- Nmap
- Gobuster
- Browser Developer Tools
- cookie manipulation
- ssh2john
- John the Ripper
- SSH
- linPEAS
- Python HTTP Server
- Netcat
- cron job abuse
- /etc/hosts manipulation
- Linux shell
- TryHackMe challenge environment

---

## Security Lessons Learned

### Authentication Security
Client-side trust creates severe authentication weaknesses.

Best practices:

- server-side session validation
- signed session tokens
- secure authentication workflows

---

### Credential Protection
Exposed SSH keys significantly increase compromise risk.

Best practices:

- secure credential storage
- private key protection
- strict access controls

---

### Scheduled Task Security
Privileged cron jobs executing remote code create dangerous escalation paths.

Best practices:

- avoid remote script execution
- secure hostname resolution
- audit scheduled tasks
- restrict writable system files

---

## Key Takeaways

This room reinforced practical understanding of:

- broken authentication exploitation
- session abuse
- credential compromise workflows
- Linux privilege escalation
- cron job hijacking
- realistic offensive attack chaining
