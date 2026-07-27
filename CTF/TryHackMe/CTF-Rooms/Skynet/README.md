# Skynet

## Overview

Skynet is a classic Easy Linux challenge that combines network enumeration, SMB enumeration, web application assessment, credential discovery, and Linux privilege escalation.

The room requires combining information gathered from multiple services to fully compromise the target.

---

## Learning Objectives

- Enumerate exposed services
- Discover SMB shares
- Gather credentials
- Enumerate web applications
- Obtain initial access
- Escalate privileges

---

## Skills Practiced

- Nmap Enumeration
- SMB Enumeration
- Web Enumeration
- Directory Discovery
- Credential Discovery
- Linux Privilege Escalation

---

## Tools Used

- Nmap
- Gobuster
- SMBClient
- Netcat
- Linux Enumeration Tools

---

## High-Level Attack Flow

1. Network Enumeration
2. SMB Enumeration
3. Credential Discovery
4. Web Application Enumeration
5. Initial Access
6. Linux Privilege Escalation
7. Root Access

---

## Key Takeaways

- SMB shares frequently expose valuable information during internal assessments.
- Web enumeration can reveal hidden attack vectors.
- Combining information from multiple services is often required to compromise a target.
- Proper privilege escalation enumeration is essential after obtaining a shell.