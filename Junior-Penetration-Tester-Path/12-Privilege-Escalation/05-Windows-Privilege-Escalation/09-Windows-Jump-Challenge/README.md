# 09-Windows-Jump-Challenge/README.md

# Windows Jump Challenge

## Overview

This challenge combines the techniques introduced throughout the Windows Privilege Escalation room into a complete assessment.

Starting with a standard user account, the objective is to enumerate the system, identify privilege escalation opportunities, exploit the appropriate weakness, and obtain administrative access.

---

## Learning Objectives

- Apply Windows enumeration
- Identify privilege escalation vectors
- Combine multiple techniques
- Gain Administrator or SYSTEM access

---

## Suggested Methodology

```text
Gain Initial Access
        ↓
Enumerate Windows
        ↓
Harvest Credentials
        ↓
Check Services
        ↓
Review Scheduled Tasks
        ↓
Enumerate Privileges
        ↓
Check Installed Software
        ↓
Run Enumeration Tools
        ↓
Exploit
        ↓
Administrator
        ↓
SYSTEM
```

---

## Areas to Investigate

Review:

- User privileges
- Windows services
- Scheduled tasks
- Credentials
- Installed software
- Registry
- Dangerous privileges
- Missing patches

---

## Skills Practiced

- Windows Enumeration
- Privilege Escalation
- WinPEAS
- Service Enumeration
- Credential Hunting
- Exploit Validation

---

## Key Takeaways

- Successful privilege escalation depends on combining multiple enumeration techniques.
- Automation complements—but does not replace—manual analysis.
- Careful methodology produces more reliable results than relying on a single exploit.