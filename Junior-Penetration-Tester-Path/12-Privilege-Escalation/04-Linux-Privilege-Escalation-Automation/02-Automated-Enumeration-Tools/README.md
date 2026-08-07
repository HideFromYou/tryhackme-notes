# 02-Automated-Enumeration-Tools/README.md

# Automated Enumeration Tools

## Overview

Several open-source tools automate Linux privilege escalation enumeration by collecting information about the operating system, permissions, services, scheduled tasks, credentials, kernel versions, and other common escalation vectors.

These tools significantly reduce enumeration time but require careful interpretation of their results.

---

## Learning Objectives

- Learn common enumeration tools
- Understand their strengths
- Interpret automated findings
- Validate reported issues

---

## LinPEAS

One of the most widely used Linux privilege escalation scripts.

Checks include:

- SUID binaries
- Writable files
- Capabilities
- Cron jobs
- Credentials
- Services
- Kernel information
- Interesting files

Repository:

```text
PEASS-ng
```

---

## LinEnum

Legacy enumeration script that gathers:

- Users
- Groups
- Permissions
- Installed software
- Scheduled tasks
- Environment variables

---

## Linux Smart Enumeration (LSE)

Designed to minimise false positives.

Provides:

- Security scores
- Categorised findings
- Easy-to-read output

---

## Linux Exploit Suggester

Matches:

- Kernel version
- Distribution
- Installed packages

Against known public privilege escalation exploits.

---

## Good Practice

Automated findings should be:

1. Verified manually
2. Confirmed to be exploitable
3. Prioritised based on impact

---

## Workflow

```text
Run Tool
      ↓
Collect Findings
      ↓
Review Output
      ↓
Validate
      ↓
Exploit
```

---

## Skills Practiced

- LinPEAS
- LinEnum
- Linux Smart Enumeration
- Linux Exploit Suggester

---

## Key Takeaways

- Enumeration tools dramatically speed up host assessment.
- False positives are common.
- Manual validation remains essential before exploitation.