# TryHackMe - Agent Sudo

## Overview
Completed the Agent Sudo TryHackMe challenge room, focusing on reconnaissance, credential discovery, steganography, Linux enumeration, and privilege escalation.

This challenge simulated a realistic attack chain from initial reconnaissance to full system compromise.

---

## Skills Practiced

- Service enumeration
- Web reconnaissance
- User-Agent manipulation
- FTP brute forcing
- Steganography analysis
- Password cracking
- Linux enumeration
- Privilege escalation
- SSH access
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and attack vectors.

Actions included:

- network scanning
- web inspection
- HTTP header manipulation
- service enumeration

This phase revealed useful attack surface and clues.

---

### Initial Access
Custom HTTP request manipulation revealed hidden information requiring a modified User-Agent.

Additional enumeration led to credential discovery opportunities.

Access was achieved through discovered credentials and remote login.

---

### Credential Discovery
Multiple techniques were required to recover credentials:

- FTP brute force
- hidden file extraction
- steganography analysis
- password cracking
- encoded data decoding

This demonstrated layered attack chaining.

---

### Linux Enumeration
After obtaining access, Linux privilege enumeration identified escalation opportunities.

Key enumeration:

```bash
sudo -l
```

This revealed exploitable sudo permissions.

---

### Privilege Escalation
Privilege escalation was achieved through sudo misconfiguration exploitation.

Technique:

```text
CVE-2019-14287
```

This allowed privilege escalation to root and full system compromise.

---

### Post-Exploitation
After escalation, restricted files were accessed and challenge objectives completed.

Activities included:

- privilege verification
- sensitive file access
- final flag retrieval

---

## Tools Used

- Nmap
- curl (custom User-Agent)
- Hydra (FTP brute force)
- FTP
- binwalk
- 7z
- steghide
- zip2john
- John the Ripper
- base64 decoding
- SSH
- sudo
- Linux shell
- CVE-2019-14287 exploitation
- TryHackMe challenge environment

---

## Security Lessons Learned

### Enumeration is Critical
Seemingly small clues can build a full attack chain.

---

### Credential Security
Weak passwords, exposed files, and recoverable secrets create major attack opportunities.

Best practices:

- strong password policies
- MFA
- credential rotation
- brute-force protections

---

### Privilege Management
Improper sudo configurations can directly result in root compromise.

Best practices:

- least privilege
- patched sudo versions
- regular privilege audits

---

## Key Takeaways

This room reinforced practical understanding of:

- attack chaining
- enumeration methodology
- credential compromise workflows
- steganography in offensive security
- Linux privilege escalation
- exploiting privilege misconfigurations
