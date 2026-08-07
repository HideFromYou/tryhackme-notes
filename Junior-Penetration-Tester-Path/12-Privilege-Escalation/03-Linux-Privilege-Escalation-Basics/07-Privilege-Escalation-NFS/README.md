# 07-Privilege-Escalation-NFS/README.md

# Privilege Escalation — NFS

## Overview

Network File System (NFS) allows directories to be shared across systems.

An insecure export using **no_root_squash** allows a remote root user to create files that remain owned by root on the target system, potentially leading to privilege escalation.

---

## Learning Objectives

- Understand NFS exports
- Identify insecure shares
- Exploit no_root_squash
- Obtain root privileges

---

## Enumerate Exports

Display exported shares:

```bash
showmount -e TARGET_IP
```

---

## Dangerous Configuration

```text
no_root_squash
```

This option prevents root privileges from being mapped to an unprivileged user.

---

## Typical Attack

```text
Mount NFS Share
        ↓
Create Root-Owned SUID Binary
        ↓
Unmount Share
        ↓
Execute Binary on Target
        ↓
Root Shell
```

---

## Skills Practiced

- NFS Enumeration
- Share Mounting
- SUID Creation
- Privilege Escalation

---

## Key Takeaways

- `no_root_squash` is one of the most dangerous NFS configurations.
- Remote root users can create privileged files on the exported filesystem.
- NFS exports should always be configured with secure permission mappings.