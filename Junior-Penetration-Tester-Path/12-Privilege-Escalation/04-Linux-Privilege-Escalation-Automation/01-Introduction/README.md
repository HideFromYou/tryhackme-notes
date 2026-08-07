# 01-Introduction/README.md

# Introduction

## Overview

Manual enumeration is essential, but modern Linux systems often contain hundreds of files, services, permissions, and configuration settings.

Automation helps penetration testers quickly identify common privilege escalation vectors, highlight suspicious configurations, and reduce the time spent performing repetitive checks. However, automated tools should support—not replace—manual analysis.

---

## Learning Objectives

- Understand the role of automation
- Learn when to use automated tools
- Recognise the limitations of automation
- Prepare for automated privilege escalation techniques

---

## Why Automation?

Automated tools can rapidly identify:

- SUID binaries
- Writable files
- Misconfigured permissions
- Capabilities
- Cron jobs
- Installed software
- Kernel information
- Interesting services

Instead of manually checking dozens of commands, a single tool can collect this information within seconds.

---

## Manual vs Automated Enumeration

### Manual

Advantages:

- Better understanding
- Fewer false positives
- Greater flexibility

Disadvantages:

- Time-consuming
- Easy to overlook findings

---

### Automated

Advantages:

- Fast
- Consistent
- Comprehensive

Disadvantages:

- False positives
- Information overload
- Requires manual validation

---

## Workflow

```text
Initial Access
       ↓
Manual Enumeration
       ↓
Automated Enumeration
       ↓
Validate Findings
       ↓
Privilege Escalation
```

---

## Key Takeaways

- Automation accelerates privilege escalation assessments.
- Automated findings should always be verified manually.
- Effective penetration testers combine automation with manual investigation.