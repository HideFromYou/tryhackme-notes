# 04-pspy-Unprivileged-Process-Monitoring/README.md

# pspy — Unprivileged Process Monitoring

## Overview

`pspy` is a lightweight Linux process monitoring tool that allows users **without root privileges** to observe processes as they are created.

Unlike `ps`, which only displays currently running processes, `pspy` continuously watches the system and reveals short-lived privileged processes such as cron jobs, maintenance scripts, and administrative commands.

This makes it particularly valuable during Linux privilege escalation.

---

## Learning Objectives

- Understand how pspy works
- Monitor privileged processes
- Identify scheduled tasks
- Discover privilege escalation opportunities

---

## Why Use pspy?

Many privileged processes execute for only a fraction of a second.

Examples include:

- Cron jobs
- Backup scripts
- Log rotation
- Maintenance scripts
- Monitoring agents

Traditional enumeration may never capture them.

---

## Running pspy

After downloading the correct binary:

```bash
chmod +x pspy64

./pspy64
```

The tool immediately begins monitoring new processes.

---

## Typical Output

Example:

```text
CMD: UID=0 PID=1034 | /usr/bin/bash /opt/scripts/backup.sh
```

Useful information includes:

- User ID
- Process ID
- Executed command
- Parent process

---

## What to Look For

Interesting findings include:

- Root-owned scripts
- Writable scripts
- Temporary files
- Backup jobs
- Automated maintenance
- Unexpected binaries

These may indicate privilege escalation vectors.

---

## Workflow

```text
Run pspy
      ↓
Observe Processes
      ↓
Identify Privileged Script
      ↓
Inspect Permissions
      ↓
Exploit Misconfiguration
```

---

## Skills Practiced

- Process Monitoring
- Linux Enumeration
- Privileged Process Analysis
- Cron Discovery

---

## Key Takeaways

- pspy requires no root privileges.
- It reveals short-lived privileged processes that static tools often miss.
- Process monitoring frequently exposes cron jobs and automated scripts suitable for privilege escalation.