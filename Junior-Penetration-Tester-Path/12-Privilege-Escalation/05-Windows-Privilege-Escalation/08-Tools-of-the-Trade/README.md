# 08-Tools-of-the-Trade/README.md

# Tools of the Trade

## Overview

While manual enumeration remains essential, several tools can significantly reduce the time required to identify Windows privilege escalation opportunities.

These tools automate many of the checks performed manually, including service enumeration, permissions analysis, missing security patches, dangerous privileges, and vulnerable software. They should assist—not replace—the penetration tester's manual analysis. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

- Understand common Windows privilege escalation tools
- Learn when to use each tool
- Interpret automated findings
- Combine automation with manual verification

---

## WinPEAS

**WinPEAS** is one of the most popular Windows privilege escalation enumeration tools.

It collects information including:

- Services
- Registry
- Scheduled Tasks
- Permissions
- Installed software
- Credentials
- Windows privileges
- Interesting files

Example:

```cmd
winpeas.exe > output.txt
```

Saving the output makes reviewing the results easier. :contentReference[oaicite:1]{index=1}

---

## PrivescCheck

**PrivescCheck** is a PowerShell-based privilege escalation enumeration script.

Advantages:

- Does not require a compiled executable
- Searches for common Windows privilege escalation vectors
- Produces structured output

Example:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force

. .\PrivescCheck.ps1

Invoke-PrivescCheck
```

:contentReference[oaicite:2]{index=2}

---

## WES-NG

**Windows Exploit Suggester – Next Generation (WES-NG)** runs on the attacker's machine rather than the target.

Workflow:

```text
Target
   ↓
systeminfo
   ↓
Save Output
   ↓
Transfer File
   ↓
wes.py
```

Example:

```bash
wes.py systeminfo.txt
```

WES-NG compares the system against known Windows vulnerabilities and missing patches. :contentReference[oaicite:3]{index=3}

---

## Metasploit Local Exploit Suggester

If a Meterpreter session already exists:

```text
multi/recon/local_exploit_suggester
```

The module analyses the target and suggests local privilege escalation exploits that may apply. :contentReference[oaicite:4]{index=4}

---

## Workflow

```text
Manual Enumeration
        ↓
Run WinPEAS
        ↓
Run PrivescCheck
        ↓
Check Missing Patches
        ↓
Validate Findings
        ↓
Privilege Escalation
```

---

## Skills Practiced

- WinPEAS
- PrivescCheck
- WES-NG
- Metasploit
- Automated Enumeration

---

## Key Takeaways

- Automated tools greatly accelerate Windows privilege escalation assessments.
- Every automated finding should be validated manually.
- Combining multiple tools provides better coverage than relying on only one.