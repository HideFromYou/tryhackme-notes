# TryHackMe - Ignite

## Overview
Completed the Ignite TryHackMe challenge room, focusing on web enumeration, CMS vulnerability exploitation, remote code execution, Linux post-exploitation, and privilege escalation through credential reuse.

This challenge simulated a realistic web application compromise from initial reconnaissance to root access.

---

## Skills Practiced

- Network reconnaissance
- Web enumeration
- robots.txt inspection
- CMS fingerprinting
- Vulnerability research
- Remote Code Execution (RCE)
- Reverse shell access
- Linux enumeration
- Credential discovery
- Privilege escalation
- Post-exploitation methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying exposed services and web application attack surface.

Discovered services included:

- HTTP
- Apache web server
- Fuel CMS application

Web inspection revealed useful information regarding the CMS version and administrative paths.

Key discovery:

```text
robots.txt
/fuel
```

This established the initial attack vector.

---

### Vulnerability Discovery
Version enumeration identified the target as Fuel CMS 1.4.1.

Research confirmed a known vulnerability:

```text
CVE-2018-16763
```

This vulnerability allows unauthenticated Remote Code Execution (RCE).

Exploit research was performed using:

- Searchsploit
- Exploit-DB references

---

### Exploitation
A public exploit targeting Fuel CMS was used to gain code execution.

This provided command execution as:

```text
www-data
```

Validation included:

- whoami
- id
- filesystem enumeration

This established the initial foothold.

---

### Post-Exploitation
After gaining shell access, local enumeration identified sensitive application files.

Credential discovery focused on:

```text
fuel/application/config/database.php
```

This exposed reusable credentials and application secrets.

A reverse shell was used to improve shell stability and interactivity.

---

### Privilege Escalation
Privilege escalation was achieved through credential reuse.

Recovered credentials were reused for privileged access.

Additional shell improvements were required to obtain interactive terminal functionality.

Activities included:

- pseudo-TTY spawning
- privilege verification
- root shell access

This resulted in full compromise.

---

## Tools Used

- Nmap
- Browser
- robots.txt inspection
- Searchsploit
- Exploit-DB
- Python RCE exploit
- Netcat
- Linux shell
- reverse shell techniques
- pseudo-TTY spawning
- credential reuse
- TryHackMe challenge environment

---

## Security Lessons Learned

### Patch Management
Running vulnerable CMS versions exposes systems to publicly available exploitation.

Best practices:

- patch management
- software version monitoring
- removing outdated CMS deployments

---

### Sensitive Configuration Exposure
Application config files often expose critical secrets.

Best practices:

- secure file permissions
- secret management
- avoid credential reuse

---

### Credential Reuse Risk
Reused credentials can turn limited compromise into full root access.

Best practices:

- unique credentials
- password rotation
- least privilege access

---

## Key Takeaways

This room reinforced practical understanding of:

- CMS enumeration
- exploit research
- remote code execution workflows
- post-exploitation credential discovery
- privilege escalation through credential misuse
- realistic offensive web security attack chains
