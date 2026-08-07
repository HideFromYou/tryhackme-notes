# README.md

# Host & Server Configuration Reviews

## Overview

This room introduces **host and server configuration reviews**, a fundamental privilege escalation methodology that focuses on identifying insecure system configurations rather than software vulnerabilities.

Instead of exploiting CVEs, penetration testers frequently escalate privileges by abusing weak permissions, insecure services, poor credential storage, scheduled tasks, or other configuration mistakes left by administrators.

The room also introduces security baselines, compliance frameworks, automated auditing tools, and structured host enumeration methodologies that will be used throughout the Privilege Escalation module.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand configuration reviews
- Differentiate vulnerabilities from misconfigurations
- Understand security baselines
- Read CIS Benchmark recommendations
- Interpret compliance reports
- Identify common categories of privilege escalation
- Apply structured host enumeration

---

# Room Structure

## 01. Introduction

Introduces configuration reviews and explains why misconfigurations remain one of the most common privilege escalation vectors.

---

## 02. What is a Configuration Review

Explains configuration reviews, their objectives, and how they differ from traditional vulnerability assessments.

---

## 03. Security Baselines and Frameworks

Introduces:

- CIS Benchmarks
- DISA STIGs
- PCI-DSS
- ISO 27001
- NIST

---

## 04. Automated Compliance Tooling

Introduces:

- Nessus
- Lynis
- OpenSCAP
- CIS-CAT

and explains how penetration testers can interpret compliance findings.

---

## 05. Categories of Misconfiguration

Explores common privilege escalation categories including permissions, credentials, services, scheduled tasks, and network configuration.

---

## 06. Structured Enumeration Methodology

Introduces a repeatable methodology for reviewing host configurations systematically.

---

## 07. Reading a CIS Benchmark

Explains how to interpret benchmark recommendations from both defensive and offensive perspectives.

---

## 08. Practical

Applies benchmark analysis against multiple Linux and Windows hosts.

---

## 09. Conclusion

Summarises configuration reviews and prepares for Linux privilege escalation.

---

## Skills Practiced

- Configuration Reviews
- Security Baselines
- CIS Benchmarks
- DISA STIGs
- Compliance Auditing
- Host Enumeration
- Privilege Escalation Methodology

---

## Workflow

```text
Identify Host
       ↓
Enumerate Configuration
       ↓
Compare to Security Baseline
       ↓
Identify Misconfiguration
       ↓
Assess Exploitability
       ↓
Privilege Escalation
```

---

## Key Takeaways

- Most privilege escalation opportunities originate from insecure configurations rather than software vulnerabilities.
- Security baselines provide measurable standards for secure system configuration.
- Compliance tools automate host auditing.
- Structured enumeration greatly improves consistency during privilege escalation assessments.