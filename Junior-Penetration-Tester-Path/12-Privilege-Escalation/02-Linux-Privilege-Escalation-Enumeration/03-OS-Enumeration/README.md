# 03-OS-Enumeration/README.md

# OS Enumeration

## Overview

Operating system enumeration collects information about the Linux host, including its hostname, kernel version, operating system release, running processes, scheduled tasks, and installed software. These details help identify potential privilege escalation vectors and vulnerable components. :contentReference[oaicite:3]{index=3}

---

## Hostname

Display:

```bash
hostname
```

May reveal:

- Server role
- Naming conventions
- Environment information

---

## Kernel Information

```bash
uname -a
```

Useful for:

- Kernel version
- Architecture
- Potential kernel exploits

---

## Kernel Build Information

```bash
cat /proc/version
```

Provides:

- Kernel version
- Compiler
- Build information

---

## Operating System Version

```bash
cat /etc/issue
```

Displays the Linux distribution and version.

---

## Running Processes

Basic:

```bash
ps
```

Detailed:

```bash
ps aux
```

Tree view:

```bash
ps axjf
```

Review running services for:

- Privileged processes
- Unusual applications
- Third-party software

---

## Scheduled Tasks

Inspect:

```bash
cat /etc/crontab
```

Also review:

- `/etc/cron.d/`
- `/var/spool/cron/`

Look for scripts executed by privileged users.

---

## Installed Packages

```bash
dpkg -l
```

Useful for:

- Installed software
- Version identification
- Vulnerable applications

---

## Skills Practiced

- Host Identification
- Kernel Enumeration
- Process Enumeration
- Cron Enumeration
- Package Enumeration

---

## Key Takeaways

- Kernel information is essential when evaluating kernel exploits.
- Running processes often reveal valuable services.
- Scheduled tasks may expose privilege escalation opportunities.
- Installed software should always be reviewed during enumeration. :contentReference[oaicite:4]{index=4}