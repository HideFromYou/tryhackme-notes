# 03-Security-Baselines-and-Frameworks/README.md

# Security Baselines and Frameworks

## Overview

A **security baseline** defines the expected secure configuration of a system. Rather than relying on personal judgement, organisations adopt recognised frameworks that specify measurable configuration requirements for operating systems, applications, and network devices. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

- Understand security baselines
- Learn major hardening frameworks
- Understand compliance profiles
- Apply baselines during assessments

---

## CIS Benchmarks

Published by the **Center for Internet Security (CIS)**.

Provide:

- Hardening recommendations
- Audit procedures
- Remediation guidance
- Security rationale

Profiles:

### Level 1

- Practical
- Low operational impact

### Level 2

- Stronger hardening
- Greater operational impact

---

## DISA STIGs

Published by the **Defense Information Systems Agency**.

Primarily used within U.S. government environments.

Severity levels:

- CAT I
- CAT II
- CAT III

CAT I represents the highest risk.

---

## Relationship to Compliance

Security baselines support larger frameworks such as:

- PCI-DSS
- ISO 27001
- NIST 800-53

These standards frequently reference CIS Benchmarks or STIG recommendations.

---

## Offensive Perspective

Penetration testers use these frameworks to:

- Understand expected secure configurations
- Identify deviations
- Prioritise exploitable findings

---

## Skills Practiced

- CIS Benchmarks
- DISA STIGs
- Host Hardening

---

## Key Takeaways

- Security baselines define secure system configurations.
- CIS Benchmarks are widely used across industry.
- DISA STIGs provide stricter government hardening guidance.
- Deviations from adopted baselines often become defensible penetration testing findings. :contentReference[oaicite:1]{index=1}