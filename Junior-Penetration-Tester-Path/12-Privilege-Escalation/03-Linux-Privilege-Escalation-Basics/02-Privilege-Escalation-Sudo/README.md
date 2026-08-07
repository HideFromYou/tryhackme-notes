# 02-Privilege-Escalation-Sudo/README.md

# Privilege Escalation — Sudo

## Overview

`sudo` allows users to execute commands as another user, typically **root**.

Improper sudo configurations can allow low-privileged users to execute privileged programs or even obtain a root shell.

---

## Learning Objectives

- Enumerate sudo permissions
- Identify dangerous sudo entries
- Exploit insecure sudo configurations
- Understand GTFOBins usage

---

## Enumerate sudo Permissions

```bash
sudo -l
```

Displays:

- Allowed commands
- Target user
- Environment restrictions

---

## Common Misconfigurations

Examples include:

- Running editors as root
- Running scripting languages
- Passwordless sudo
- Wildcard rules
- Misconfigured binaries

---

## GTFOBins

GTFOBins documents legitimate binaries that can be abused for privilege escalation.

Examples include:

- vim
- less
- find
- awk
- tar
- perl
- python

---

## Typical Workflow

```text
sudo -l
      ↓
Identify Allowed Binary
      ↓
Search GTFOBins
      ↓
Execute Escape
      ↓
Root Shell
```

---

## Skills Practiced

- sudo Enumeration
- GTFOBins
- Privilege Escalation

---

## Key Takeaways

- `sudo -l` should always be one of the first commands executed.
- Legitimate administrative tools can often be abused to obtain root.
- GTFOBins provides documented privilege escalation techniques for many common binaries.