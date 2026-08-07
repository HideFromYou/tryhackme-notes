# Linux Privilege Escalation Automation

## Overview

This room introduces **automation techniques** that accelerate Linux privilege escalation after manual enumeration has been completed.

Rather than replacing manual analysis, automation helps quickly identify common misconfigurations, discover known privilege escalation vectors, monitor privileged processes, and correlate findings with public exploits. The room covers automated enumeration tools, public exploit research, **pspy** for process monitoring, and a practical challenge to combine these techniques.

---

# Learning Objectives

After completing this room, you should be able to:

- Understand the role of automation during privilege escalation
- Use automated Linux enumeration tools
- Identify and validate public privilege escalation exploits
- Monitor privileged processes without root access
- Combine manual and automated techniques during assessments

---

# Room Structure

## 01. Introduction

Introduces automation in Linux privilege escalation and explains why it complements, rather than replaces, manual enumeration.

---

## 02. Automated Enumeration Tools

Covers popular enumeration tools including:

- LinPEAS
- LinEnum
- Linux Smart Enumeration (LSE)
- Linux Exploit Suggester

Focuses on interpreting tool output instead of blindly trusting it.

---

## 03. Privilege Escalation — Public Exploits

Introduces responsible identification and validation of public privilege escalation exploits using:

- CVEs
- Searchsploit
- Exploit-DB
- GitHub PoCs

---

## 04. pspy — Unprivileged Process Monitoring

Explains how **pspy** monitors running processes without requiring root privileges, helping identify privileged cron jobs, scripts, and services.

---

## 05. Challenge

Applies the techniques learned throughout the room against a Linux target to identify and exploit a privilege escalation vector.

---

## 06. Conclusion

Summarises automation techniques and prepares for Windows Privilege Escalation.

---

## Skills Practiced

- Linux Enumeration
- Automated Enumeration
- LinPEAS
- Linux Exploit Suggester
- Searchsploit
- CVE Research
- pspy
- Process Monitoring
- Privilege Escalation

---

## Workflow

```text
Gain Initial Access
        ↓
Manual Enumeration
        ↓
Run Enumeration Tools
        ↓
Validate Findings
        ↓
Research Public Exploits
        ↓
Monitor Processes
        ↓
Exploit Privilege Escalation
        ↓
Obtain Root
```

---

## Key Takeaways

- Automation accelerates enumeration but does not replace understanding.
- Enumeration tools frequently highlight findings that require manual verification.
- Public exploits should always be validated against the target before use.
- Process monitoring tools like **pspy** can reveal privilege escalation opportunities that static enumeration may miss.
- Successful privilege escalation combines **manual analysis**, **automation**, and **critical thinking** rather than relying on a single tool.