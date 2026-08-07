# README.md

# Linux Privilege Escalation Basics

## Overview

This room builds directly on the **Linux Privilege Escalation: Enumeration** room.

Instead of identifying potential privilege escalation vectors, the focus now shifts to **exploiting** them. You will abuse common Linux misconfigurations to escalate from a low-privileged user to **root**, using practical techniques that appear frequently during penetration tests and CTFs. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this room, you should be able to:

- Exploit common Linux privilege escalation vectors
- Abuse insecure sudo configurations
- Exploit vulnerable SUID binaries
- Perform PATH hijacking
- Abuse Linux capabilities
- Exploit writable cron jobs
- Abuse insecure NFS configurations

---

# Room Structure

## 01. Introduction

Introduces the practical Linux privilege escalation room and explains how it builds on manual enumeration.

---

## 02. Privilege Escalation: Sudo

Learn how misconfigured sudo permissions allow low-privileged users to execute commands as root.

---

## 03. Privilege Escalation: SUID

Exploit SUID binaries that execute with the permissions of their owner.

---

## 04. Privilege Escalation: PATH

Abuse PATH environment variable hijacking to execute attacker-controlled binaries.

---

## 05. Privilege Escalation: Capabilities

Exploit Linux capabilities assigned to executables instead of full root privileges.

---

## 06. Privilege Escalation: Cron Jobs

Abuse writable scripts executed automatically by privileged cron jobs.

---

## 07. Privilege Escalation: NFS

Exploit insecure **no_root_squash** NFS exports to obtain root access.

---

## 08. Conclusion

Summarises the Linux privilege escalation techniques introduced throughout the room.

---

## Skills Practiced

- Linux Privilege Escalation
- sudo
- SUID
- PATH Hijacking
- Linux Capabilities
- Cron Jobs
- NFS Misconfiguration

---

## Workflow

```text
Initial Access
      ↓
Enumeration
      ↓
Identify Misconfiguration
      ↓
Exploit Privilege Escalation Vector
      ↓
Obtain Root Shell
```

---

## Key Takeaways

- Most Linux privilege escalation paths originate from insecure configurations rather than software vulnerabilities.
- Enumeration directly feeds exploitation.
- Small permission mistakes often lead to complete system compromise.