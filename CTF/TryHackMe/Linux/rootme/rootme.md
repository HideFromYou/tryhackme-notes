# TryHackMe - RootMe

## Overview
Completed the RootMe TryHackMe challenge room, focusing on web enumeration, file upload bypass, reverse shell exploitation, Linux enumeration, and privilege escalation through SUID misconfiguration.

This challenge simulated a realistic web exploitation workflow leading to root compromise.

---

## Skills Practiced

- Network reconnaissance
- Web enumeration
- Directory brute forcing
- File upload exploitation
- Filter bypass techniques
- Reverse shell deployment
- Linux enumeration
- SUID exploitation
- GTFOBins usage
- Privilege escalation
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and web application attack surface.

Discovered services included:

- SSH
- HTTP

Web enumeration revealed hidden application functionality and upload capabilities.

This established the primary attack path.

---

### Web Enumeration
Directory brute forcing identified useful application paths.

Key discoveries included:

- file upload functionality
- uploaded file access paths
- publicly reachable application resources

This revealed a direct exploitation opportunity.

---

### File Upload Exploitation
The application exposed file upload functionality with weak extension filtering.

A malicious PHP reverse shell payload was prepared and the upload filter was bypassed using alternative executable file extensions.

Techniques included:

- file extension bypass
- upload abuse
- remote payload execution

This provided initial shell access.

---

### Initial Access
Uploaded payload execution resulted in reverse shell access.

Activities included:

- shell stabilization
- user context verification
- filesystem enumeration

This established the initial foothold.

---

### Linux Enumeration
Post-exploitation enumeration focused on identifying privilege escalation opportunities.

Activities included:

- privilege inspection
- SUID binary discovery
- executable abuse analysis

---

### Privilege Escalation
Privilege escalation was achieved through abuse of an SUID Python binary.

Key finding:

```bash
find / -user root -perm /4000 2>/dev/null
```

Exploitation used GTFOBins methodology to spawn a privileged shell.

This resulted in root compromise.

---

## Tools Used

- Nmap
- Gobuster
- PHP reverse shell
- file upload bypass techniques
- Netcat
- Linux shell
- SUID enumeration
- GTFOBins
- Python
- TryHackMe challenge environment

---

## Security Lessons Learned

### File Upload Security
Weak upload validation can directly lead to remote code execution.

Best practices:

- strict extension validation
- MIME type validation
- content inspection
- execution isolation

---

### Privilege Management
SUID misconfigurations create dangerous privilege escalation opportunities.

Best practices:

- least privilege
- SUID auditing
- unnecessary binary removal
- privilege monitoring

---

### Post-Exploitation Awareness
Limited initial access can often be escalated through system misconfiguration.

---

## Key Takeaways

This room reinforced practical understanding of:

- web exploitation workflows
- upload filter bypass techniques
- reverse shell operations
- Linux privilege escalation
- SUID exploitation
- realistic offensive attack chaining
