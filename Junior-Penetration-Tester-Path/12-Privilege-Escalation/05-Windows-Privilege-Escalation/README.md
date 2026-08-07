# README.md

# Windows Privilege Escalation

## Overview

This room introduces the most common privilege escalation techniques found in Windows environments.

Starting from a standard user account, you will learn how attackers identify weaknesses that allow them to obtain administrative or even **SYSTEM** privileges. The room covers credential harvesting, service misconfigurations, dangerous Windows privileges, vulnerable software, automated enumeration tools, and practical privilege escalation scenarios. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

---

# Learning Objectives

After completing this room, you should be able to:

- Understand Windows privilege escalation
- Identify Windows account types
- Harvest credentials from common locations
- Exploit service misconfigurations
- Abuse dangerous Windows privileges
- Exploit vulnerable software
- Use automated Windows enumeration tools
- Perform practical Windows privilege escalation

---

# Room Structure

## 01. Introduction

Introduces Windows privilege escalation and explains why an initial low-privileged foothold is only the beginning of an attack.

---

## 02. Windows Privilege Escalation

Explains:

- Windows account types
- Administrators
- Standard Users
- SYSTEM
- Local Service
- Network Service

---

## 03. Harvesting Passwords from Usual Spots

Explores common locations where credentials are accidentally stored.

---

## 04. Other Quick Wins

Covers simple privilege escalation opportunities including:

- Scheduled Tasks
- AlwaysInstallElevated

---

## 05. Abusing Service Misconfigurations

Focuses on insecure Windows services and service permissions.

---

## 06. Abusing Dangerous Privileges

Explains Windows privileges that can be abused to gain elevated access.

---

## 07. Abusing Vulnerable Software

Demonstrates privilege escalation through vulnerable third-party software and missing patches.

---

## 08. Tools of the Trade

Introduces:

- WinPEAS
- PrivescCheck
- WES-NG
- Metasploit Local Exploit Suggester

---

## 09. Windows Jump Challenge

Combines all previous techniques into a practical Windows privilege escalation exercise.

---

## 10. Conclusion

Summarises the Windows privilege escalation methodology.

---

## Skills Practiced

- Windows Privilege Escalation
- Windows Enumeration
- Credential Harvesting
- Service Exploitation
- Windows Privileges
- Vulnerability Assessment
- WinPEAS
- WES-NG
- PrivescCheck

---

## Workflow

```text
Initial User Access
        ↓
System Enumeration
        ↓
Identify Weakness
        ↓
Exploit Privilege Escalation Vector
        ↓
Administrator
        ↓
SYSTEM
```

---

## Key Takeaways

- Windows privilege escalation relies heavily on host enumeration.
- Misconfigurations frequently provide easier escalation paths than software exploits.
- Automated tools accelerate discovery but require manual validation.
- Understanding Windows security mechanisms is essential for successful privilege escalation.