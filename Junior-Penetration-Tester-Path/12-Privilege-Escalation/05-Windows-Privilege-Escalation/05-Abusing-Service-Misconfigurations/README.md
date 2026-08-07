# 05-Abusing-Service-Misconfigurations/README.md

# Abusing Service Misconfigurations

## Overview

Windows services frequently execute with elevated privileges.

If a service is improperly configured, attackers may be able to modify its executable, change its configuration, or abuse weak permissions to execute arbitrary code as **Administrator** or **SYSTEM**.

---

## Learning Objectives

- Enumerate Windows services
- Identify insecure service permissions
- Understand unquoted service paths
- Exploit writable service binaries

---

## Windows Services

Useful commands:

```cmd
sc query
```

Detailed information:

```cmd
sc qc <service>
```

---

## Common Misconfigurations

Examples include:

- Writable service binaries
- Writable service directories
- Weak service permissions
- Unquoted service paths
- Weak registry permissions

---

## Writable Service Binary

Workflow:

```text
Enumerate Services
        ↓
Find Writable Binary
        ↓
Replace Binary
        ↓
Restart Service
        ↓
SYSTEM Shell
```

---

## Unquoted Service Paths

Example:

```text
C:\Program Files\Example Service\service.exe
```

Without quotation marks, Windows may execute attacker-controlled binaries placed earlier in the search path.

---

## Enumeration

Useful commands:

```cmd
sc qc

wmic service

accesschk
```

---

## Skills Practiced

- Service Enumeration
- Service Permissions
- Windows Services
- SYSTEM Privilege Escalation

---

## Key Takeaways

- Services often execute with elevated privileges.
- Weak service permissions frequently result in SYSTEM access.
- Service enumeration should always be included during Windows privilege escalation.