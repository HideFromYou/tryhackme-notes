# 06-Privilege-Escalation-Cron-Jobs/README.md

# Privilege Escalation — Cron Jobs

## Overview

Cron is the Linux task scheduler.

If a privileged cron job executes a writable script or binary, an attacker may modify that file and execute arbitrary commands with elevated privileges.

---

## Learning Objectives

- Enumerate cron jobs
- Identify writable scheduled tasks
- Exploit insecure cron configurations

---

## View System Cron

```bash
cat /etc/crontab
```

Also inspect:

```text
/etc/cron.d/
/etc/cron.daily/
/etc/cron.hourly/
/var/spool/cron/
```

---

## What to Look For

Review:

- Writable scripts
- Writable binaries
- Weak permissions
- Commands executed as root

---

## Attack Workflow

```text
Enumerate Cron Jobs
         ↓
Locate Writable Script
         ↓
Insert Malicious Command
         ↓
Cron Executes
         ↓
Gain Root
```

---

## Skills Practiced

- Cron Enumeration
- Permission Analysis
- Scheduled Task Exploitation

---

## Key Takeaways

- Cron jobs frequently execute with elevated privileges.
- Writable scripts executed by root represent a common privilege escalation vector.
- Scheduled tasks should always reference protected files with secure permissions.