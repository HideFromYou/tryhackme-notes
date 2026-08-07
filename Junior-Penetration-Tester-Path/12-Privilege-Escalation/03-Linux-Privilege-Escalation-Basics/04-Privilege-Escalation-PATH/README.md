# 04-Privilege-Escalation-PATH/README.md

# Privilege Escalation — PATH

## Overview

Linux searches directories listed in the **PATH** environment variable when executing commands without specifying an absolute path.

If a privileged script calls a program by name rather than by full path, an attacker may be able to replace that program with a malicious executable.

---

## Learning Objectives

- Understand PATH resolution
- Identify vulnerable scripts
- Perform PATH hijacking
- Gain privileged execution

---

## View PATH

```bash
echo $PATH
```

---

## Vulnerable Example

Instead of:

```bash
/usr/bin/id
```

A script executes:

```bash
id
```

Linux searches each directory in `$PATH` until it finds a matching executable.

---

## Attack Concept

```text
Writable Directory
        ↓
Create Fake Binary
        ↓
Modify PATH
        ↓
Privileged Script Executes
        ↓
Malicious Binary Runs
```

---

## Requirements

Generally requires:

- Writable directory
- PATH control
- Privileged script
- Missing absolute paths

---

## Skills Practiced

- PATH Enumeration
- Environment Variables
- Binary Hijacking

---

## Key Takeaways

- PATH hijacking abuses command lookup order.
- Administrative scripts should always use absolute paths.
- Writable directories earlier in PATH present significant security risks.