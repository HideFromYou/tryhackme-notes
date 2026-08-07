# Privilege Escalation

## Overview

This section of the **Junior Penetration Tester Path** focuses on one of the most important phases of a penetration test: **Privilege Escalation**.

After obtaining an initial foothold on a target system, attackers attempt to elevate their privileges to gain administrative or root-level access. This module covers both **Linux** and **Windows** privilege escalation methodologies, beginning with configuration reviews and manual enumeration before progressing to practical exploitation and automated tooling.

Rather than relying on a single exploit, successful privilege escalation combines **systematic enumeration**, **misconfiguration analysis**, **public exploit research**, and **careful validation**.

---

# Learning Objectives

After completing this module, you should be able to:

- Perform structured host configuration reviews
- Identify privilege escalation opportunities on Linux
- Enumerate Linux systems manually
- Exploit common Linux privilege escalation vectors
- Use automated Linux privilege escalation tools
- Perform Windows privilege escalation
- Harvest credentials from insecure locations
- Exploit Windows service misconfigurations
- Abuse dangerous Windows privileges
- Identify vulnerable software
- Use Windows privilege escalation automation tools
- Apply repeatable privilege escalation methodologies

---

# Module Structure

## 01. Host & Server Configuration Reviews

Introduces security configuration reviews and explains how insecure configurations frequently lead to privilege escalation.

### Topics

- Configuration Reviews
- Security Baselines
- CIS Benchmarks
- Compliance Frameworks
- Automated Compliance Tools
- Configuration Enumeration
- Practical Configuration Reviews

---

## 02. Linux Privilege Escalation — Enumeration

Introduces manual Linux enumeration techniques used to identify privilege escalation vectors.

### Topics

- OS Enumeration
- User Enumeration
- Network Enumeration
- File Enumeration
- Privilege Escalation Methodology

---

## 03. Linux Privilege Escalation — Basics

Covers the most common Linux privilege escalation techniques.

### Topics

- sudo
- SUID
- PATH Hijacking
- Linux Capabilities
- Cron Jobs
- NFS Misconfigurations

---

## 04. Linux Privilege Escalation — Automation

Introduces tools that accelerate Linux privilege escalation.

### Topics

- LinPEAS
- LinEnum
- Linux Smart Enumeration
- Linux Exploit Suggester
- Searchsploit
- Public Exploits
- pspy
- Process Monitoring

---

## 05. Windows Privilege Escalation

Introduces privilege escalation techniques specific to Windows environments.

### Topics

- Windows Account Types
- Credential Harvesting
- Scheduled Tasks
- AlwaysInstallElevated
- Service Misconfigurations
- Dangerous Privileges
- Vulnerable Software
- WinPEAS
- PrivescCheck
- WES-NG
- Windows Jump Challenge

---

# Core Workflow

```text
Gain Initial Access
        ↓
Host Enumeration
        ↓
Configuration Review
        ↓
Identify Misconfiguration
        ↓
Validate Finding
        ↓
Research Public Exploits
        ↓
Exploit Privilege Escalation
        ↓
Administrator / Root
        ↓
SYSTEM (Windows)
        ↓
Post Exploitation
```

---

# Tools Covered

## Linux

### Manual Enumeration

- hostname
- uname
- ps
- find
- id
- env
- sudo
- getcap
- ss
- ip

### Automated Enumeration

- LinPEAS
- LinEnum
- Linux Smart Enumeration (LSE)
- Linux Exploit Suggester
- pspy

---

## Windows

### Manual Enumeration

- whoami
- whoami /priv
- icacls
- sc
- schtasks
- reg
- systeminfo
- wmic

### Automated Enumeration

- WinPEAS
- PrivescCheck
- WES-NG
- Metasploit Local Exploit Suggester

---

## Research Tools

- Searchsploit
- Exploit-DB
- GTFOBins
- CVE Database
- Public Proof-of-Concept Repositories

---

# Skills Practiced

- Host Enumeration
- Configuration Reviews
- Linux Privilege Escalation
- Windows Privilege Escalation
- Manual Enumeration
- Automated Enumeration
- Credential Harvesting
- Service Enumeration
- Service Exploitation
- Scheduled Task Abuse
- Linux Capabilities
- SUID Exploitation
- PATH Hijacking
- NFS Exploitation
- Process Monitoring
- CVE Research
- Searchsploit
- WinPEAS
- WES-NG
- GTFOBins
- Privilege Validation
- Root Shell Acquisition
- SYSTEM Privilege Escalation

---

# Methodology

```text
Enumerate
     ↓
Understand
     ↓
Validate
     ↓
Exploit
     ↓
Escalate
     ↓
Verify Access
     ↓
Document Findings
```

---

# Key Takeaways

- Privilege escalation almost always begins with **thorough enumeration**.
- Configuration mistakes are often more valuable than software vulnerabilities.
- Linux and Windows each provide multiple privilege escalation vectors, but both require the same disciplined methodology.
- Automated tools accelerate enumeration, but manual validation remains essential.
- Public exploits should always be verified against the target before execution.
- Successful privilege escalation combines **enumeration**, **critical thinking**, and **careful exploitation** rather than relying solely on automated tools.
- Mastering these techniques provides the foundation for **Active Directory security testing**, **lateral movement**, and more advanced penetration testing scenarios.

---

## Module Outcome

After completing **Privilege Escalation**, you should be comfortable progressing from a low-privileged foothold to administrative access by systematically identifying and exploiting Linux and Windows privilege escalation opportunities while following a professional penetration testing methodology.