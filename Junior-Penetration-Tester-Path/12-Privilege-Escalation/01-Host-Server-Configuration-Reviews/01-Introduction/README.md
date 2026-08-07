# 01-Introduction/README.md

# Introduction

## Overview

Privilege escalation often relies on configuration weaknesses rather than software vulnerabilities.

Modern operating systems contain hundreds of configurable settings, and insecure defaults or administrator mistakes frequently provide attackers with opportunities to gain elevated privileges.

Configuration reviews provide a structured method for identifying these weaknesses before exploitation.

---

## Learning Objectives

- Understand configuration reviews
- Differentiate vulnerabilities from misconfigurations
- Prepare for structured enumeration

---

## Main Concepts

Privilege escalation opportunities commonly arise from:

- Weak permissions
- Insecure services
- Misconfigured scheduled tasks
- Poor credential storage
- Excessive privileges

Rather than searching only for missing patches, penetration testers must also evaluate how securely the host has been configured.

---

## Workflow

```text
Access Host
      ↓
Review Configuration
      ↓
Identify Weaknesses
      ↓
Validate Finding
      ↓
Escalate Privileges
```

---

## Key Takeaways

- Configuration weaknesses are among the most reliable privilege escalation vectors.
- Systematic reviews produce more consistent results than ad-hoc enumeration.