# Privilege Escalation - TryHackMe Junior Penetration Tester

## Overview

This repository contains my notes and learning outcomes from the **Privilege Escalation** module of the **TryHackMe Junior Penetration Tester** learning path.

The module focuses on understanding privilege escalation across both **Linux** and **Windows** environments, covering manual enumeration, automated enumeration, common privilege escalation vectors, and realistic challenge labs.

> **Disclaimer**
>
> This repository contains only educational notes and summaries.
> No TryHackMe flags, walkthroughs, or challenge solutions are included.

---

# Skills Gained

- Linux Privilege Escalation
- Windows Privilege Escalation
- Manual Enumeration
- Automated Enumeration
- Host Configuration Review
- Security Baselines
- Misconfiguration Assessment
- SUID Exploitation
- Linux Capabilities
- PATH Hijacking
- Cron Job Exploitation
- NFS Misconfiguration
- Password Harvesting
- Windows Service Misconfiguration
- Windows Privilege Abuse
- Public Exploit Research
- Process Monitoring
- Privilege Escalation Methodology

---

# Module Content

## 1. Host-Server Configuration Reviews

Learned how to assess operating system configurations against security baselines.

Topics covered:

- Configuration Reviews
- Security Baselines
- CIS Benchmarks
- Compliance Frameworks
- Automated Compliance Tools
- Configuration Misconfigurations
- Structured Enumeration Methodology

---

## 2. Linux Privilege Escalation – Enumeration

Focused on collecting information before attempting privilege escalation.

Enumeration areas:

- Operating System
- Kernel Version
- Installed Packages
- Users and Groups
- Running Processes
- Scheduled Tasks
- Network Configuration
- Mounted Drives
- Sensitive Files
- Permissions

---

## 3. Linux Privilege Escalation – Basics

Hands-on practice with common Linux privilege escalation techniques.

Techniques covered:

- sudo misconfigurations
- SUID binaries
- PATH hijacking
- Linux Capabilities
- Cron Jobs
- NFS misconfigurations

---

## 4. Linux Privilege Escalation – Automation

Focused on speeding up privilege escalation assessments using automation.

Tools and techniques:

- LinPEAS
- LinEnum
- pspy
- Public exploit identification
- Manual verification of findings

---

## 5. Windows Privilege Escalation

Learned the most common Windows privilege escalation vectors.

Topics included:

- Enumeration
- Password Harvesting
- Registry Secrets
- PowerShell History
- Configuration Files
- Saved Credentials
- Service Misconfigurations
- Dangerous Windows Privileges
- Vulnerable Software
- Windows Privilege Escalation Tools

---

## 6. Linux Privilege Escalation Challenge

Applied the complete methodology in a realistic Linux machine.

Objectives:

- Perform enumeration
- Identify attack vectors
- Escalate privileges
- Obtain root access

---

## 7. Windows Privilege Escalation Challenge

Applied Windows privilege escalation techniques in a realistic environment.

Objectives:

- Enumerate the system
- Identify privilege escalation opportunities
- Escalate from Guest/User to SYSTEM

---

# Tools Used

### Linux

- LinPEAS
- LinEnum
- pspy
- find
- grep
- sudo
- getcap
- cron
- systemctl

### Windows

- winPEAS
- PowerShell
- cmd
- reg
- schtasks
- accesschk
- icacls

---

# Methodology

My privilege escalation workflow generally follows these steps:

1. Enumeration
2. Identify Misconfigurations
3. Validate Findings
4. Exploit Safely
5. Gain Elevated Privileges
6. Document Findings

---

# Key Takeaways

Throughout this module I strengthened my understanding of:

- Manual enumeration before exploitation
- Linux privilege escalation vectors
- Windows privilege escalation techniques
- Host configuration reviews
- Security baselines
- Automated enumeration tools
- Identifying insecure configurations
- Applying structured privilege escalation methodology

---

## Learning Platform

- TryHackMe
- Junior Penetration Tester Path

---

## Repository Status

Completed
