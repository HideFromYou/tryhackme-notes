# 03-Privilege-Escalation-SUID/README.md

# Privilege Escalation — SUID

## Overview

The **Set User ID (SUID)** permission allows an executable to run with the privileges of its owner rather than the user executing it.

If a privileged executable is vulnerable or misconfigured, it may provide a path to root.

---

## Learning Objectives

- Understand SUID
- Enumerate SUID binaries
- Identify exploitable binaries
- Abuse GTFOBins entries

---

## Find SUID Files

```bash
find / -perm -4000 -type f 2>/dev/null
```

---

## Why SUID is Dangerous

When a root-owned binary has the SUID bit set:

```text
Normal User
      ↓
Execute Binary
      ↓
Runs as Root
```

---

## GTFOBins

Many common binaries have documented SUID privilege escalation techniques.

Examples:

- find
- vim
- bash
- cp
- env
- python

---

## Workflow

```text
Locate SUID Binary
        ↓
Identify Binary
        ↓
Check GTFOBins
        ↓
Exploit
        ↓
Root Shell
```

---

## Skills Practiced

- SUID Enumeration
- File Permissions
- GTFOBins

---

## Key Takeaways

- SUID binaries execute using the owner's privileges.
- Root-owned SUID binaries deserve careful investigation.
- GTFOBins greatly simplifies identifying exploitable binaries.