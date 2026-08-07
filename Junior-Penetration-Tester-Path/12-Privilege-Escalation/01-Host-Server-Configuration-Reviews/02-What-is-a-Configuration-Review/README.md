# 02-What-is-a-Configuration-Review/README.md

# What is a Configuration Review

## Overview

A configuration review evaluates whether a system has been configured according to accepted security standards.

Unlike vulnerability assessments that focus on software flaws, configuration reviews examine how the operating system, services, permissions, authentication, and security settings have been implemented.

---

## Learning Objectives

- Understand configuration reviews
- Differentiate configuration issues from vulnerabilities
- Recognise common review objectives

---

## Configuration Review

Configuration reviews examine:

- User accounts
- Permissions
- Authentication
- Services
- Scheduled tasks
- Network settings
- Credential storage

The goal is to identify deviations from secure configuration baselines.

---

## Vulnerability vs Misconfiguration

### Vulnerability

A flaw in software.

Example:

```text
Unpatched CVE
```

### Misconfiguration

An insecure administrative setting.

Examples:

- Writable sensitive files
- Weak permissions
- Enabled root login
- Weak password policy

---

## Why They Matter

Configuration weaknesses:

- Are extremely common
- Often survive patching
- Can directly enable privilege escalation

---

## Skills Practiced

- Configuration Analysis
- Security Reviews
- Host Assessment

---

## Key Takeaways

- Configuration reviews evaluate system hardening.
- Misconfigurations frequently lead to privilege escalation.
- Secure configuration is as important as software patching.