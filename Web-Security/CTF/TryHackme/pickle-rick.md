# TryHackMe - Pickle Rick

## Overview
Completed the Pickle Rick TryHackMe challenge room, focusing on web enumeration, hidden resource discovery, authentication bypass through exposed credentials, command injection exploitation, and Linux privilege escalation.

This challenge simulated a beginner-friendly offensive web exploitation workflow leading to root compromise.

---

## Skills Practiced

- Network reconnaissance
- Web enumeration
- Directory brute forcing
- Source code inspection
- Credential discovery
- Authentication abuse
- Command injection exploitation
- Reverse shell techniques
- Linux enumeration
- Privilege escalation
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and web application attack surface.

Discovered services included:

- SSH
- HTTP

Web enumeration established the primary attack path.

---

### Web Enumeration
Application inspection revealed useful exposed information.

Discovery techniques included:

- HTML source inspection
- robots.txt analysis
- directory brute forcing

Recovered information included:

- usernames
- passwords
- hidden application functionality

This established authenticated access opportunities.

---

### Authentication Access
Recovered credentials were used to access a restricted command panel.

This demonstrated insecure credential exposure and weak access control.

---

### Command Injection Exploitation
The application exposed a web-based command execution interface.

This allowed arbitrary system command execution.

Activities included:

- user context validation
- filesystem enumeration
- restricted file access
- command execution abuse

This established shell-level access.

---

### Post-Exploitation
Multiple challenge objectives required filesystem discovery and restricted file access.

Techniques included:

- directory traversal
- command-line file reading
- optional reverse shell deployment

---

### Privilege Escalation
Privilege enumeration revealed dangerous sudo permissions.

Key finding:

```bash
sudo -l
```

Result:

```text
NOPASSWD: ALL
```

This allowed unrestricted root command execution and full system compromise.

---

## Tools Used

- Nmap
- Gobuster
- ffuf
- Browser
- HTML source inspection
- robots.txt enumeration
- web shell interaction
- reverse shell techniques
- Netcat
- Linux shell
- sudo
- linPEAS
- TryHackMe challenge environment

---

## Security Lessons Learned

### Credential Exposure
Hardcoded or publicly exposed credentials create immediate compromise risk.

Best practices:

- never expose secrets client-side
- secure authentication storage
- proper credential management

---

### Command Injection
Exposing command execution functionality creates severe remote compromise risk.

Best practices:

- sanitize user input
- avoid direct shell execution
- least privilege service accounts

---

### Privilege Management
Unrestricted sudo access directly results in root compromise.

Best practices:

- least privilege
- sudo permission audits
- restricted command execution

---

## Key Takeaways

This room reinforced practical understanding of:

- web enumeration workflows
- credential discovery
- command injection exploitation
- Linux privilege escalation
- offensive attack chaining
