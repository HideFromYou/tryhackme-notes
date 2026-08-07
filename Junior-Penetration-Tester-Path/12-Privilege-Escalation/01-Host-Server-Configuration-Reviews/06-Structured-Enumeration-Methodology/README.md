# 06-Structured-Enumeration-Methodology/README.md

# Structured Enumeration Methodology

## Overview

Privilege escalation depends heavily on thorough enumeration.

Rather than immediately attempting exploits, penetration testers systematically gather information about the host, identify weaknesses, and prioritise findings before attempting privilege escalation.

A repeatable methodology ensures consistent results across engagements.

---

## Learning Objectives

- Understand structured enumeration
- Build repeatable workflows
- Prioritise findings
- Reduce missed opportunities

---

## Step 1 — System Information

Collect:

- Operating system
- Version
- Architecture
- Hostname
- Installed patches

---

## Step 2 — Users and Groups

Identify:

- Current user
- Group memberships
- Administrators
- Service accounts

---

## Step 3 — Services

Review:

- Running services
- Startup configuration
- Service permissions
- Service accounts

---

## Step 4 — Permissions

Inspect:

- Writable directories
- Writable executables
- Sensitive files
- Ownership

---

## Step 5 — Credentials

Search for:

- Passwords
- Keys
- Tokens
- Configuration files
- Environment variables

---

## Step 6 — Scheduled Tasks

Review:

- Cron jobs
- Timers
- Scheduled Tasks

Check whether executed files can be modified.

---

## Step 7 — Network

Review:

- Listening ports
- Shares
- Trust relationships
- Internal services

---

## Methodology

```text
System
    ↓
Users
    ↓
Services
    ↓
Permissions
    ↓
Credentials
    ↓
Scheduled Tasks
    ↓
Network
    ↓
Prioritise Findings
```

---

## Key Takeaways

- Enumeration should always follow a structured process.
- Gathering complete information is more valuable than immediately exploiting findings.
- Consistent methodology reduces human error during privilege escalation assessments.