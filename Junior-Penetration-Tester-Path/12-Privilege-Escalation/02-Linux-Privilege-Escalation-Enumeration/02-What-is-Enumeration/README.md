# 02-What-is-Enumeration/README.md

# What is Enumeration?

## Overview

Enumeration is the systematic process of collecting information about a target system after obtaining initial access.

Rather than immediately searching for exploits, penetration testers first identify operating system details, users, permissions, services, network configuration, and files that may reveal privilege escalation opportunities.

---

## Purpose

Enumeration aims to answer questions such as:

- Which operating system is running?
- Which users exist?
- Which services are active?
- Which files are accessible?
- Which permissions are misconfigured?
- Which privilege escalation vectors exist?

---

## Why It Matters

Effective enumeration:

- Reduces guesswork
- Identifies attack paths
- Reveals configuration weaknesses
- Prioritises privilege escalation opportunities

Most privilege escalation vulnerabilities are discovered through careful observation rather than automated exploitation.

---

## Enumeration Principles

- Gather information before exploiting
- Be methodical
- Document findings
- Verify observations
- Avoid assumptions

---

## Workflow

```text
Collect Information
        ↓
Analyse Findings
        ↓
Identify Weaknesses
        ↓
Prioritise Opportunities
```

---

## Key Takeaways

- Enumeration is the foundation of Linux privilege escalation.
- A structured methodology improves consistency.
- Thorough information gathering frequently reveals multiple escalation paths.