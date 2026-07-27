# Proxy

## Overview

Proxy is an Easy Active Directory challenge that focuses on Windows domain enumeration, SMB services, Kerberos authentication, delegation, and privilege escalation techniques within an enterprise environment.

The room demonstrates how multiple small findings can be chained together to compromise an Active Directory environment.

---

## Learning Objectives

- Enumerate Windows services
- Analyze SMB shares
- Capture and analyze NTLM authentication
- Perform Active Directory enumeration
- Understand Kerberos delegation
- Escalate privileges within the domain

---

## Skills Practiced

- Nmap Enumeration
- SMB Enumeration
- NTLM Authentication
- Active Directory Enumeration
- BloodHound Analysis
- Kerberos Delegation
- Windows Privilege Escalation

---

## Tools Used

- Nmap
- SMBClient
- Responder
- BloodHound
- Evil-WinRM
- RDP

---

## High-Level Attack Flow

1. Network Enumeration
2. SMB Enumeration
3. Credential Collection
4. Active Directory Enumeration
5. BloodHound Analysis
6. Kerberos Delegation Abuse
7. Privilege Escalation
8. Administrative Access

---

## Key Takeaways

- Active Directory attacks rely heavily on proper enumeration.
- BloodHound simplifies identifying privilege escalation paths.
- Kerberos delegation misconfigurations can provide powerful attack opportunities.
- Multiple low-risk findings can combine into a complete domain compromise.