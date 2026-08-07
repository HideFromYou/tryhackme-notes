# 04-Other-Quick-Wins/README.md

# Other Quick Wins

## Overview

Not every Windows privilege escalation requires exploiting a complex vulnerability.

Some systems contain simple configuration mistakes that immediately allow attackers to obtain higher privileges. While these situations are more common in CTFs and labs than real enterprise environments, they are still valuable to recognise during assessments.

This room covers two common examples:

- Scheduled Tasks
- AlwaysInstallElevated MSI installations :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

- Enumerate scheduled tasks
- Identify writable task binaries
- Understand AlwaysInstallElevated
- Recognise quick privilege escalation opportunities

---

## Scheduled Tasks

Windows Scheduled Tasks execute programs automatically using a specified user account.

Useful command:

```cmd
schtasks
```

Detailed information:

```cmd
schtasks /query /tn <taskname> /fo list /v
```

Important fields include:

- Task To Run
- Run As User

These indicate **what** executes and **which account** executes it. :contentReference[oaicite:1]{index=1}

---

## Writable Task Files

If the executable or script referenced by a scheduled task is writable by the current user:

```text
Scheduled Task
        ↓
Modify Executable
        ↓
Task Executes
        ↓
Higher-Privileged Shell
```

Always verify permissions before attempting exploitation.

---

## Checking Permissions

Example:

```cmd
icacls C:\path\to\task.bat
```

Look for write permissions granted to:

```text
BUILTIN\Users
```

---

## AlwaysInstallElevated

Windows Installer (`.msi`) packages normally execute with the privileges of the user launching them.

If the **AlwaysInstallElevated** policy is enabled, MSI packages may execute with elevated privileges.

Relevant registry locations:

```cmd
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer

reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer
```

Both registry values must be enabled before this technique is exploitable. :contentReference[oaicite:2]{index=2}

---

## Skills Practiced

- Scheduled Task Enumeration
- Permission Analysis
- MSI Privilege Escalation
- Registry Enumeration

---

## Key Takeaways

- Writable scheduled task executables are a common privilege escalation vector.
- AlwaysInstallElevated is uncommon but can provide immediate administrative execution.
- Simple configuration mistakes often provide the fastest escalation path.