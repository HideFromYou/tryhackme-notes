# 05-Privilege-Escalation-Capabilities/README.md

# Privilege Escalation — Linux Capabilities

## Overview

Linux capabilities divide the traditional root privileges into smaller, more granular permissions that can be assigned to executables. While this improves security in many cases, incorrectly assigned capabilities can still allow attackers to escalate privileges.

---

## Learning Objectives

- Understand Linux capabilities
- Enumerate capabilities
- Identify dangerous capability assignments
- Exploit misconfigured executables

---

## What are Capabilities?

Instead of granting full root privileges, Linux can assign specific privileges such as:

- Network administration
- File ownership changes
- Raw socket access
- UID manipulation

These privileges are attached directly to executables.

---

## Enumerating Capabilities

List files with capabilities:

```bash
getcap -r / 2>/dev/null
```

Review each executable carefully.

---

## Dangerous Capabilities

Common examples include:

- cap_setuid
- cap_setgid
- cap_sys_admin
- cap_dac_override

Depending on the executable, these capabilities may allow privilege escalation.

---

## Exploitation Workflow

```text
Enumerate Capabilities
         ↓
Identify Dangerous Binary
         ↓
Research Exploitation Method
         ↓
Execute Binary
         ↓
Gain Elevated Privileges
```

---

## Skills Practiced

- Capability Enumeration
- Linux Permissions
- Privilege Escalation

---

## Key Takeaways

- Capabilities provide fine-grained privileges instead of full root access.
- Misconfigured capabilities may still lead to privilege escalation.
- Enumerating capabilities should always be part of a Linux privilege escalation assessment.