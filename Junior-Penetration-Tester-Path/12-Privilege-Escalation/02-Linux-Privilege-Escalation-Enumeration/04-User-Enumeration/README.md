# 04-User-Enumeration/README.md

# User Enumeration

## Overview

User enumeration focuses on identifying local users, groups, privileges, environment variables, command history, and sudo permissions. Understanding who has access to the system and what they are allowed to do is essential when searching for privilege escalation opportunities. :contentReference[oaicite:5]{index=5}

---

## Current User

Display user information:

```bash
id
```

Shows:

- UID
- GID
- Group memberships

Other users can also be queried:

```bash
id username
```

---

## Environment Variables

```bash
env
```

Useful variables include:

- HOME
- USER
- PATH
- SHELL
- LANG

The `PATH` variable may reveal interpreters or locations useful for privilege escalation.

---

## Command History

```bash
history
```

May reveal:

- Previous commands
- Credentials
- Administrative activity

---

## Sudo Permissions

```bash
sudo -l
```

Lists commands the current user is allowed to execute with elevated privileges.

This is one of the most valuable enumeration commands.

---

## Local Users

View:

```bash
cat /etc/passwd
```

Extract usernames:

```bash
cut -d ":" -f1 /etc/passwd
```

Filter interactive users:

```bash
grep /home /etc/passwd
```

---

## Skills Practiced

- User Enumeration
- Group Enumeration
- Environment Enumeration
- Sudo Enumeration
- Account Discovery

---

## Key Takeaways

- `id` quickly identifies current privileges.
- `env` may reveal useful execution paths.
- `history` occasionally exposes sensitive information.
- `sudo -l` is one of the highest-priority privilege escalation checks.
- `/etc/passwd` provides valuable information about local accounts. :contentReference[oaicite:6]{index=6}