# 06-Abusing-Dangerous-Privileges/README.md

# Abusing Dangerous Privileges

## Overview

Windows assigns specific privileges to user accounts beyond normal group membership.

Some privileges appear harmless but can be abused to obtain elevated access when assigned incorrectly.

---

## Learning Objectives

- Enumerate Windows privileges
- Identify dangerous privileges
- Understand privilege abuse
- Escalate through privilege assignments

---

## Enumerating Privileges

Display current privileges:

```cmd
whoami /priv
```

---

## Common Dangerous Privileges

Examples include:

- SeBackupPrivilege
- SeRestorePrivilege
- SeImpersonatePrivilege
- SeAssignPrimaryTokenPrivilege
- SeTakeOwnershipPrivilege
- SeDebugPrivilege

---

## Typical Workflow

```text
Enumerate Privileges
        ↓
Identify Dangerous Privilege
        ↓
Research Abuse Technique
        ↓
Gain Elevated Access
```

---

## Why They Matter

Many Windows privileges:

- Bypass security checks
- Access protected files
- Impersonate users
- Debug privileged processes

---

## Skills Practiced

- Windows Privileges
- Privilege Enumeration
- Token Abuse

---

## Key Takeaways

- Group membership is not the only source of privilege.
- Individual Windows privileges can provide powerful escalation opportunities.
- `whoami /priv` should always be executed during enumeration.