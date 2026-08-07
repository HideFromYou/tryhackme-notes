# 02-Windows-Privilege-Escalation/README.md

# Windows Privilege Escalation

## Overview

Privilege escalation involves using an existing user account to gain access to another account with greater privileges. While the ultimate objective is usually **Administrator** or **SYSTEM**, attackers may sometimes move through several accounts before reaching full administrative control. :contentReference[oaicite:4]{index=4}

---

## Learning Objectives

- Understand Windows account types
- Identify built-in service accounts
- Recognise common privilege escalation targets

---

## Standard Users

Standard users:

- Have limited permissions
- Cannot modify critical system settings
- Can generally access only their own files

Group:

```text
Users
```

---

## Administrators

Administrators can:

- Modify system settings
- Install software
- Manage services
- Access protected files
- Create users

Group:

```text
Administrators
```

---

## SYSTEM Account

The **SYSTEM** (LocalSystem) account is managed by Windows and possesses privileges that exceed those of a normal Administrator.

Many Windows services execute using this account. :contentReference[oaicite:5]{index=5}

---

## Local Service

Characteristics:

- Minimal local privileges
- Anonymous network authentication

---

## Network Service

Characteristics:

- Minimal local privileges
- Uses computer credentials for network authentication

---

## Common Privilege Escalation Vectors

Examples include:

- Service misconfigurations
- Scheduled tasks
- Dangerous privileges
- Credential exposure
- Vulnerable software
- Missing security patches

---

## Workflow

```text
Standard User
       ↓
Identify Weakness
       ↓
Administrator
       ↓
SYSTEM
```

---

## Skills Practiced

- Windows Enumeration
- Account Identification
- Privilege Analysis

---

## Key Takeaways

- Windows contains several built-in security principals with different privilege levels.
- SYSTEM possesses greater privileges than Administrator.
- Understanding account types helps prioritise privilege escalation targets. :contentReference[oaicite:6]{index=6}