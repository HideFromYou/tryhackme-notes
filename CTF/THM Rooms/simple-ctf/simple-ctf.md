# TryHackMe - Simple CTF

## Overview
Completed the Simple CTF TryHackMe challenge room, focusing on service enumeration, web exploitation, SQL Injection vulnerability discovery, credential compromise, password cracking, and Linux privilege escalation.

This challenge simulated a realistic attack chain from reconnaissance to root compromise.

---

## Skills Practiced

- Network reconnaissance
- Service enumeration
- FTP enumeration
- Anonymous FTP access
- Web enumeration
- CMS fingerprinting
- Vulnerability research
- SQL Injection exploitation
- Password cracking
- SSH access
- Linux enumeration
- Privilege escalation
- GTFOBins usage
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and attack vectors.

Discovered services included:

- FTP
- HTTP
- SSH (non-standard port)

This established multiple attack paths.

---

### FTP Enumeration
Anonymous FTP access was enabled, exposing useful internal information.

Recovered artifacts included:

- usernames
- password hints
- internal clues

This supported credential attacks.

---

### Web Enumeration
Directory brute forcing revealed a hidden CMS application.

CMS fingerprinting identified:

```text
CMS Made Simple
```

Version discovery enabled targeted vulnerability research.

---

### Vulnerability Discovery
Research identified a known SQL Injection vulnerability affecting the discovered CMS version.

Key finding:

```text
CVE-2019-9053
```

This created a direct exploitation path.

---

### Exploitation
The SQL Injection vulnerability was exploited to recover authentication material.

Recovered information included:

- usernames
- password hashes

This enabled the credential attack phase.

---

### Password Cracking
Recovered password hashes were cracked offline using wordlist attacks.

This resulted in valid credentials for remote access.

---

### Initial Access
SSH access was obtained using compromised credentials.

This established the initial foothold.

Activities included:

- user validation
- flag retrieval
- local enumeration

---

### Privilege Escalation
Privilege enumeration revealed unsafe sudo permissions.

Key command:

```bash
sudo -l
```

Finding:

```text
vim executable with elevated privileges
```

Privilege escalation was achieved using GTFOBins methodology to spawn a root shell.

This resulted in full system compromise.

---

## Tools Used

- Nmap
- Gobuster
- FTP
- anonymous FTP login
- Searchsploit
- SQL Injection exploit
- Hashcat
- SSH
- sudo
- GTFOBins
- Linux shell
- TryHackMe challenge environment

---

## Security Lessons Learned

### Exposed Services
Anonymous FTP and unnecessary services increase attack surface.

Best practices:

- disable anonymous access
- reduce exposed services
- restrict public file access

---

### Patch Management
Outdated CMS deployments expose systems to public exploitation.

Best practices:

- regular updates
- vulnerability monitoring
- remove unsupported software

---

### Credential Security
Weak or crackable credentials lead directly to compromise.

Best practices:

- strong password policies
- MFA
- credential rotation
- password auditing

---

### Privilege Management
Unsafe sudo permissions can directly lead to root compromise.

Best practices:

- least privilege
- sudo audits
- restricted privileged binaries

---

## Key Takeaways

This room reinforced practical understanding of:

- service enumeration
- CMS exploitation workflows
- SQL Injection attack chains
- password cracking
- Linux privilege escalation
- realistic offensive security methodology
