# 01-Introduction/README.md

# Introduction

## Overview

During a penetration test, attackers frequently obtain access to Windows systems through a standard user account. While these accounts provide limited permissions, they often serve as the starting point for privilege escalation toward administrative access.

This room introduces the techniques used to move from an unprivileged Windows user to Administrator or SYSTEM where possible. :contentReference[oaicite:2]{index=2}

---

## Learning Objectives

- Understand Windows privilege escalation
- Recognise the importance of post-compromise enumeration
- Prepare for common Windows escalation techniques

---

## Initial Foothold

A standard user typically has access to:

- Personal files
- User profile
- Limited registry access
- Basic system information

Administrative actions remain restricted until privileges are elevated.

---

## Why Privilege Escalation Matters

Higher privileges allow attackers to:

- Access protected files
- Dump credentials
- Install persistence
- Disable security controls
- Execute administrative commands

---

## Workflow

```text
Gain Initial Access
        ↓
Enumerate Windows
        ↓
Identify Weakness
        ↓
Privilege Escalation
```

---

## Key Takeaways

- Initial access rarely provides complete control of a Windows system.
- Privilege escalation is often required to continue post-exploitation.
- Enumeration is the first step toward discovering escalation opportunities. :contentReference[oaicite:3]{index=3}