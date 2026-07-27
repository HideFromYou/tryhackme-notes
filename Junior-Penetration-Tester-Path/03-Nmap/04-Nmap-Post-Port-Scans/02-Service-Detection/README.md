# Service Detection

## Overview

Service detection identifies the application and version running on each open port. Version information helps determine whether a service is vulnerable to known exploits.

---

## Learning Objectives

- Detect service versions
- Adjust detection intensity
- Understand banner grabbing

---

## Basic Version Detection

```bash
sudo nmap -sV <TARGET>
```

---

## Version Intensity

Light detection:

```bash
sudo nmap -sV --version-light <TARGET>
```

Maximum detection:

```bash
sudo nmap -sV --version-all <TARGET>
```

Custom intensity:

```bash
sudo nmap -sV --version-intensity 5 <TARGET>
```

---

## Example Output

```
22/tcp  OpenSSH 9.2p1
80/tcp  nginx 1.22.1
143/tcp Dovecot imapd
```

---

## Important Notes

- `-sV` performs a full TCP connection.
- Cannot remain a stealth SYN scan.
- More accurate than guessing services by port number.

---

## Skills Practiced

- Banner Grabbing
- Version Detection
- Service Enumeration

## Key Takeaways

- `-sV` identifies application versions.
- Version information is crucial for vulnerability research.
- Detection intensity can be adjusted for speed or accuracy.