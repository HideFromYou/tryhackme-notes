# 03-Harvesting-Passwords-from-Usual-Spots/README.md

# Harvesting Passwords from Usual Spots

## Overview

Not every privilege escalation requires exploiting a vulnerability.

Credentials are frequently left behind by administrators or users inside configuration files, scripts, registry entries, scheduled tasks, backups, and command history. Simply locating these credentials may allow attackers to move directly into more privileged accounts.

---

## Learning Objectives

- Search for exposed credentials
- Identify insecure password storage
- Locate configuration files
- Review Windows credential locations

---

## Common Locations

Search for credentials inside:

- Configuration files
- Batch scripts
- PowerShell scripts
- Backup files
- Documentation
- Registry entries
- Scheduled tasks
- Desktop notes

---

## Command History

Review PowerShell history and command history for:

- Passwords
- Connection strings
- Administrative commands

---

## Registry

Interesting registry locations may contain:

- AutoLogon credentials
- Application settings
- Service passwords

---

## Configuration Files

Review:

- XML
- INI
- CONF
- TXT
- BAT
- PS1

for:

- Hardcoded credentials
- API keys
- Connection strings

---

## Workflow

```text
Enumerate Files
        ↓
Search Configuration
        ↓
Locate Credentials
        ↓
Authenticate as Higher User
```

---

## Skills Practiced

- Credential Hunting
- Windows Enumeration
- File Analysis
- Registry Enumeration

---

## Key Takeaways

- Credential harvesting is often faster than exploiting vulnerabilities.
- Administrators frequently leave sensitive information in insecure locations.
- Every configuration file should be considered a potential source of credentials.