# 05-Categories-of-Misconfiguration/README.md

# Categories of Misconfiguration

## Overview

Host configuration reviews become much more efficient when findings are grouped into categories. Rather than checking systems randomly, penetration testers examine common areas where administrator mistakes frequently introduce security weaknesses.

These categories provide a repeatable methodology for identifying privilege escalation opportunities.

---

## Learning Objectives

- Identify common misconfiguration categories
- Understand how configuration weaknesses arise
- Prioritise high-value findings
- Build a structured review process

---

## 1. User Accounts

Review:

- Local users
- Administrative accounts
- Service accounts
- Disabled accounts
- Default accounts

Look for:

- Unused privileged accounts
- Shared credentials
- Weak account management

---

## 2. Permissions

Review:

- Files
- Directories
- Services
- Registry (Windows)
- Scheduled tasks

Examples:

- Writable system files
- Excessive permissions
- Incorrect ownership

---

## 3. Authentication

Review:

- Password policies
- Password storage
- SSH configuration
- Root login
- Multi-factor authentication

Common weaknesses include weak password requirements and insecure authentication mechanisms.

---

## 4. Services

Review:

- Running services
- Startup services
- Service permissions
- Service accounts

Look for:

- Misconfigured services
- Writable service binaries
- Over-privileged service accounts

---

## 5. Scheduled Tasks

Review:

- Cron jobs
- Systemd timers
- Windows Scheduled Tasks

Important checks:

- Writable scripts
- Writable executables
- Weak permissions

---

## 6. Credentials

Search for:

- Configuration files
- Scripts
- Backup files
- Environment variables
- SSH keys

Common findings include hardcoded passwords and exposed API keys.

---

## 7. Network Configuration

Review:

- Listening services
- Firewall rules
- Trust relationships
- Open shares

Misconfigured network services may expose additional privilege escalation opportunities.

---

## Workflow

```text
Users
   ↓
Permissions
   ↓
Authentication
   ↓
Services
   ↓
Scheduled Tasks
   ↓
Credentials
   ↓
Network
```

---

## Key Takeaways

- Configuration weaknesses tend to fall into predictable categories.
- Structured reviews reduce the likelihood of overlooking privilege escalation vectors.
- Credentials, permissions, and services are among the highest-value areas to investigate.