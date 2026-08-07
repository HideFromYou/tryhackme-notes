# 07-Abusing-Vulnerable-Software/README.md

# Abusing Vulnerable Software

## Overview

Privilege escalation is sometimes achieved by exploiting vulnerable software installed on the target system.

Third-party applications, outdated drivers, and missing security patches may provide local privilege escalation opportunities.

---

## Learning Objectives

- Identify vulnerable software
- Enumerate installed applications
- Research public exploits
- Validate exploit applicability

---

## Enumeration

Review:

- Installed software
- Running services
- Software versions
- Drivers
- Windows patches

Useful commands include:

```cmd
systeminfo
```

```cmd
wmic product
```

---

## Public Exploits

Useful resources:

- CVE Database
- Exploit-DB
- Searchsploit
- GitHub Proof of Concepts

---

## Validation

Before using any exploit verify:

- Windows version
- Software version
- Architecture
- Exploit requirements

---

## Workflow

```text
Identify Software
        ↓
Determine Version
        ↓
Search Public Exploit
        ↓
Validate
        ↓
Exploit
```

---

## Skills Practiced

- Vulnerability Assessment
- CVE Research
- Searchsploit
- Exploit Validation

---

## Key Takeaways

- Vulnerable software remains an important privilege escalation vector.
- Public exploits should always be validated before execution.
- Accurate software enumeration is essential for successful exploitation.