# 06-File-Enumeration/README.md

# File Enumeration

## Overview

File enumeration identifies files, directories, permissions, ownership, and executables that may lead to privilege escalation.

Sensitive files, writable locations, SUID binaries, configuration files, and development tools are all valuable targets during Linux privilege escalation.

---

## Learning Objectives

- Enumerate files and directories
- Identify writable locations
- Locate SUID binaries
- Search for hidden files
- Discover sensitive configuration files

---

## List Files

Detailed listing:

```bash
ls -la
```

Shows:

- Permissions
- Ownership
- Hidden files

---

## Search for Files

Find specific files:

```bash
find / -name filename 2>/dev/null
```

Search by extension:

```bash
find / -name "*.conf" 2>/dev/null
```

---

## Hidden Files

Locate hidden files:

```bash
find / -name ".*" 2>/dev/null
```

These may contain:

- Credentials
- SSH keys
- Backup files
- Configuration files

---

## Writable Files

Search:

```bash
find / -writable -type f 2>/dev/null
```

Writable privileged files may enable privilege escalation.

---

## SUID Binaries

Locate SUID executables:

```bash
find / -perm -4000 -type f 2>/dev/null
```

Review each binary against known privilege escalation techniques.

---

## Interesting Files

Search for:

- Configuration files
- Scripts
- Backup archives
- Development projects
- Database credentials
- SSH keys

Examples:

```text
*.conf
*.bak
*.sql
*.pem
*.key
```

---

## Development Tools

Check for:

- gcc
- make
- python
- perl
- ruby

These may simplify exploitation.

---

## Skills Practiced

- File Enumeration
- Permission Analysis
- SUID Enumeration
- Sensitive File Discovery

---

## Key Takeaways

- File permissions are a major source of privilege escalation.
- SUID binaries should always be reviewed carefully.
- Hidden files often contain valuable information.
- Development tools can greatly expand exploitation options.