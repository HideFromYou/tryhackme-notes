# 01-Introduction/README.md

# Introduction

## Overview

Privilege escalation is a process rather than a single exploit. Success depends on the specific configuration of the target system, including its kernel version, installed applications, supported programming languages, permissions, and user configuration. This room introduces the manual enumeration techniques required before attempting privilege escalation. :contentReference[oaicite:1]{index=1}

---

## What is Privilege Escalation?

Privilege escalation is the process of moving from a lower-privileged account to a higher-privileged one by exploiting:

- Vulnerabilities
- Design flaws
- Configuration mistakes

The goal is to obtain access to resources normally restricted to administrators.

---

## Why Enumeration Matters

Most real-world engagements begin with a low-privileged user account.

Enumeration helps identify opportunities to:

- Reset passwords
- Bypass access controls
- Modify configurations
- Establish persistence
- Execute administrative commands

---

## Learning Objectives

- Understand Linux privilege escalation
- Learn manual enumeration
- Identify potential escalation vectors

---

## Workflow

```text
Gain Initial Access
        ↓
Enumerate System
        ↓
Identify Weaknesses
        ↓
Privilege Escalation
```

---

## Key Takeaways

- Privilege escalation depends on understanding the target system.
- Enumeration should always be performed before attempting exploitation.
- Every piece of collected information may contribute to discovering an escalation path. :contentReference[oaicite:2]{index=2}