# README.md

# Linux Privilege Escalation — Enumeration

## Overview

Enumeration is the foundation of every successful Linux privilege escalation assessment.

Rather than immediately searching for exploits, penetration testers first collect as much information as possible about the operating system, users, services, network configuration, files, and installed software. Most privilege escalation paths are discovered through careful enumeration rather than exploitation.

This room introduces the manual enumeration techniques that will be used throughout the Linux Privilege Escalation module. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this room, you should be able to:

- Understand the role of enumeration in privilege escalation
- Gather operating system information
- Enumerate users and groups
- Inspect network configuration
- Locate sensitive and hidden files
- Identify potential privilege escalation vectors manually

---

# Room Structure

## 01. Introduction

Introduces Linux privilege escalation and explains why enumeration is the most important phase.

---

## 02. What is Enumeration?

Explains the purpose of enumeration and the methodology used before attempting privilege escalation.

---

## 03. OS Enumeration

Covers:

- hostname
- uname
- /proc/version
- /etc/issue
- ps
- cron
- dpkg

---

## 04. User Enumeration

Covers:

- id
- env
- history
- sudo -l
- /etc/passwd

---

## 05. Network Enumeration

Introduces:

- ifconfig
- ip addr
- netstat
- ss

---

## 06. File Enumeration

Focuses on:

- ls -la
- find
- Hidden files
- Writable files
- SUID files
- Interesting development tools

---

## 07. Conclusion

Summarises manual Linux enumeration techniques.

---

## Skills Practiced

- Linux Enumeration
- OS Enumeration
- User Enumeration
- Network Enumeration
- File Enumeration
- Privilege Escalation Methodology

---

## Enumeration Workflow

```text
Operating System
        ↓
Users & Groups
        ↓
Network
        ↓
Files & Permissions
        ↓
Potential Privilege Escalation Vectors
```

---

## Key Takeaways

- Enumeration is the most important stage of Linux privilege escalation.
- Manual enumeration builds a complete understanding of the target.
- Small configuration details frequently reveal escalation opportunities.
- Thorough enumeration often removes the need for guesswork later in the assessment.