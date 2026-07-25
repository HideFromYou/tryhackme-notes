# TryHackMe - LazyAdmin

## Overview
Completed the LazyAdmin TryHackMe challenge room, focusing on web enumeration, CMS exploitation, credential discovery, reverse shell access, and Linux privilege escalation through writable script abuse.

This challenge simulated a realistic web application compromise workflow from reconnaissance to root access.

---

## Skills Practiced

- Network reconnaissance
- Web enumeration
- Directory brute forcing
- CMS fingerprinting
- Vulnerability research
- Hash cracking
- Reverse shell exploitation
- Linux enumeration
- Privilege escalation
- Writable script abuse
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and web application attack surface.

Discovered services included:

- SSH
- HTTP
- Apache web server

Web enumeration revealed hidden application directories and CMS assets.

This established the attack surface.

---

### Web Enumeration
Directory discovery identified hidden paths within the web application.

Further inspection revealed:

- administrative panels
- CMS assets
- backup-related files
- exposed application components

CMS fingerprinting identified:

```text
SweetRice CMS
```

This enabled targeted vulnerability research.

---

### Credential Discovery
Exposed backup data revealed administrative credential material.

Recovered credentials included password hashes, which were cracked offline.

This enabled authenticated administrative access.

---

### Exploitation
Authenticated access was leveraged to achieve remote code execution.

Techniques involved:

- CMS exploitation
- PHP payload execution
- reverse shell deployment

This provided initial shell access to the target.

---

### Linux Enumeration
Post-exploitation enumeration identified privilege escalation opportunities.

Activities included:

- file permission inspection
- script analysis
- writable path discovery
- privilege verification

---

### Privilege Escalation
Privilege escalation was achieved through abuse of a writable script executed with elevated privileges.

A writable backup-related script allowed arbitrary command execution as root.

This resulted in full compromise.

---

## Tools Used

- Nmap
- Gobuster
- Searchsploit
- Browser
- SweetRice CMS exploit techniques
- MD5 hash cracking
- CrackStation
- Netcat
- reverse shell payloads
- Linux shell
- file permission enumeration
- writable script abuse
- TryHackMe challenge environment

---

## Security Lessons Learned

### Backup Exposure
Publicly accessible backup files can leak sensitive credentials.

Best practices:

- secure backup storage
- restricted file permissions
- prevent web-accessible backups

---

### CMS Security
Outdated CMS platforms can expose exploitable vulnerabilities.

Best practices:

- patch management
- version monitoring
- remove unused components

---

### Privilege Management
Writable scripts executed by privileged processes create direct escalation paths.

Best practices:

- least privilege
- file integrity monitoring
- restrict writable privileged scripts

---

## Key Takeaways

This room reinforced practical understanding of:

- web application enumeration
- CMS exploitation workflows
- credential recovery
- reverse shell operations
- Linux privilege escalation through misconfiguration
- realistic offensive attack chaining
