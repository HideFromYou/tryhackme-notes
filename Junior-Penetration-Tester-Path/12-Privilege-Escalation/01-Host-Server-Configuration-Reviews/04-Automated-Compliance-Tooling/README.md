# 04-Automated-Compliance-Tooling/README.md

# Automated Compliance Tooling

## Overview

Large environments cannot realistically be audited manually. Automated compliance tools compare host configurations against recognised security baselines and produce reports highlighting failed checks, helping both defenders and penetration testers identify configuration weaknesses efficiently. :contentReference[oaicite:2]{index=2}

---

## Learning Objectives

- Understand compliance tools
- Compare common auditing solutions
- Interpret compliance reports
- Understand offensive enumeration tools

---

## Nessus

Commercial vulnerability scanner from Tenable.

Supports:

- CIS Benchmarks
- DISA STIGs
- Custom compliance policies

Produces:

- Pass/Fail results
- Remediation guidance

---

## Lynis

Open-source host auditing tool.

Runs locally on:

- Linux
- macOS
- Unix

Provides:

- Hardening score
- Findings
- Warnings
- Recommendations

---

## OpenSCAP

Implements:

```text
SCAP
```

Used for automated compliance evaluation against structured benchmark content.

---

## CIS-CAT

Official CIS assessment tool.

Designed specifically for:

- CIS Benchmarks

Produces detailed benchmark compliance reports.

---

## Offensive Enumeration

Tools such as:

- LinPEAS
- WinPEAS
- PowerUp

Identify many of the same configuration issues but present them from an attacker's perspective.

---

## Skills Practiced

- Nessus
- Lynis
- OpenSCAP
- CIS-CAT
- Compliance Reporting

---

## Key Takeaways

- Automated compliance tools reduce manual auditing effort.
- Compliance reports can reveal privilege escalation opportunities.
- Offensive enumeration tools and compliance tools often detect the same underlying issues from different perspectives. :contentReference[oaicite:3]{index=3}