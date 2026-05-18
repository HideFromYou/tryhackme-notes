# TryHackMe - Bounty Hacker

## Overview
Completed the Bounty Hacker TryHackMe challenge room, focusing on FTP enumeration, credential discovery, SSH brute forcing, Linux privilege escalation, and post-exploitation.

This challenge simulated a practical boot2root workflow from service enumeration to root compromise.

---

## Skills Practiced

- Network reconnaissance
- Service enumeration
- FTP enumeration
- Anonymous FTP access
- Credential discovery
- SSH brute forcing
- Linux enumeration
- Privilege escalation
- GTFOBins exploitation
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and attack opportunities.

Discovered services included:

- FTP
- SSH
- HTTP

This established multiple possible attack vectors.

---

### FTP Enumeration
Anonymous FTP access was enabled, allowing unauthenticated access to downloadable files.

This exposed useful internal information, including:

- usernames
- password wordlists
- operational hints

This provided a direct path toward credential attacks.

---

### Credential Discovery
Recovered FTP files contained useful authentication information.

This enabled targeted brute force attacks against SSH using discovered usernames and password candidates.

---

### Initial Access
SSH brute forcing successfully recovered valid credentials.

Access was obtained via:

```bash
ssh user@target
```

This established the initial foothold.

---

### Linux Enumeration
After obtaining shell access, privilege enumeration was performed.

Key command:

```bash
sudo -l
```

This revealed dangerous sudo permissions.

---

### Privilege Escalation
Privilege escalation was achieved through a sudo misconfiguration involving tar.

Technique used:

GTFOBins sudo tar shell escape:

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

This resulted in root shell access.

---

### Post-Exploitation
After privilege escalation, restricted files were accessed and challenge objectives were completed.

Activities included:

- privilege verification
- root filesystem access
- final flag retrieval

---

## Tools Used

- Nmap
- Gobuster
- FTP
- Anonymous FTP login
- Hydra
- SSH
- sudo
- GTFOBins
- Linux shell
- TryHackMe challenge environment

---

## Security Lessons Learned

### Exposed Services
Anonymous FTP access can expose sensitive internal information.

Best practices:

- disable anonymous access
- restrict file permissions
- monitor FTP activity

---

### Credential Security
Exposed usernames and weak passwords dramatically increase attack success.

Best practices:

- strong password policies
- MFA
- brute-force protections
- credential rotation

---

### Privilege Management
Unsafe sudo permissions can directly lead to root compromise.

Best practices:

- least privilege
- sudo permission reviews
- restricted binary execution

---

## Key Takeaways

This room reinforced practical understanding of:

- attack path identification
- credential-based compromise
- Linux privilege escalation methodology
- GTFOBins abuse
- realistic offensive security workflow
