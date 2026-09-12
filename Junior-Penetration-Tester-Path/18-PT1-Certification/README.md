# TryHackMe PT1 - Junior Penetration Tester Certification

## Overview

This folder documents my preparation and practical experience from the **TryHackMe Junior Penetration Tester (PT1) Certification**.

PT1 is a hands-on practical penetration testing certification designed to simulate a real-world penetration testing engagement.

The exam is completed within a **48-hour window** and covers three major technical areas:

- Web Application Security
- Network Penetration Testing
- Active Directory

The assessment is not based on multiple-choice or theory questions. The focus is on identifying vulnerabilities, exploiting them, documenting the attack path, and producing a professional penetration testing report.

## Certification Structure

```text
PT1 Certification
│
├── 01 - Web
│   └── Web Application Penetration Testing
│
├── 02 - Network
│   └── Network Penetration Testing
│
└── 03 - Active Directory
    └── Active Directory Security Testing
```

## 01 - Web

The Web stage focused on identifying and exploiting vulnerabilities in a web application.

Topics and techniques relevant to this stage included:

- Reconnaissance and enumeration
- Authentication testing
- SQL Injection
- Cross-Site Scripting
- Broken Access Control
- Mass Assignment
- Session and token handling
- API security testing
- Business logic vulnerabilities
- Command Injection
- Exploitation through Burp Suite
- Manual request manipulation

The goal was not simply to identify vulnerabilities, but to understand their impact and prove them through exploitation.

[Web Stage →](./01-Web/)

## 02 - Network

The Network stage focused on identifying exposed network services and determining whether they could be exploited.

Topics included:

- Host discovery
- Port scanning
- Service enumeration
- Version detection
- Banner grabbing
- SMB
- FTP
- SSH
- Other exposed network services
- Credential attacks
- Service exploitation
- Privilege escalation
- Lateral movement
- Post-exploitation

The methodology followed the general penetration testing workflow:

```text
Reconnaissance
      ↓
Port Scanning
      ↓
Service Enumeration
      ↓
Vulnerability Identification
      ↓
Exploitation
      ↓
Initial Access
      ↓
Privilege Escalation
      ↓
Post-Exploitation
```

[Network Stage →](./02-Network/)

## 03 - Active Directory

The Active Directory stage focused on attacking an enterprise Windows domain environment.

Topics relevant to the assessment included:

- Active Directory enumeration
- LDAP
- Kerberos
- Domain users and groups
- Authentication mechanisms
- Credential harvesting
- BloodHound
- Misconfigured permissions
- Privilege escalation
- Lateral movement
- Pass-the-Hash
- Pass-the-Ticket
- Kerberoasting
- AS-REP Roasting
- Domain privilege escalation

The objective was to understand the relationships between users, computers, groups and permissions and identify a viable attack path through the domain.

[Active Directory Stage →](./03-Active-Directory/)

## Reporting

Reporting was an important part of the certification.

For each significant vulnerability, I needed to think beyond simply obtaining a flag or gaining access.

A proper finding should explain:

- What the vulnerability is
- Where it exists
- How it was identified
- How it can be exploited
- Evidence of exploitation
- Security impact
- Recommended remediation

This reflects the difference between simply completing a CTF and performing a professional penetration test.

## My PT1 Approach

During the assessment, my methodology was based around maintaining a structured workflow rather than randomly trying exploits.

```text
Understand the Scope
        ↓
Reconnaissance
        ↓
Enumeration
        ↓
Identify Attack Surface
        ↓
Test Hypotheses
        ↓
Exploit
        ↓
Establish Access
        ↓
Enumerate Again
        ↓
Privilege Escalation
        ↓
Lateral Movement
        ↓
Validate Impact
        ↓
Document Findings
        ↓
Write Report
```

A key lesson from PT1 was that obtaining initial access is often only the beginning of the attack.

After every successful compromise, I needed to stop and ask:

> What does this access give me?

Then I continued enumerating the new environment from the perspective of the compromised user.

## Purpose of This Folder

This section of my repository is different from the normal TryHackMe room writeups.

The CTF rooms document individual vulnerable machines and specific techniques.

This folder documents my **actual PT1 certification experience**, including:

- Exam structure
- Attack methodology
- Findings
- Evidence
- Exploitation
- Lessons learned
- Reporting
- Practical observations from the assessment

The objective is to preserve what I learned from the certification and create a reference that I can use when preparing for future penetration testing engagements and interviews.

## Official PT1 Context

TryHackMe describes PT1 as an entry-level, hands-on offensive security certification covering **web, network and Active Directory** environments.

The current Jr Penetration Tester learning path is designed as the canonical preparation route for PT1 and includes dedicated Web Security, Active Directory, penetration testing methodology and reporting content, as well as practical capstone challenges.

## Final Takeaway

PT1 was an important transition from learning individual penetration testing techniques to applying them as part of a complete engagement.

The most important lesson was not a particular tool or exploit.

It was learning to think in terms of an attack chain:

```text
Information
    ↓
Attack Surface
    ↓
Vulnerability
    ↓
Exploitation
    ↓
Access
    ↓
Privilege
    ↓
Impact
    ↓
Evidence
    ↓
Professional Report
```

This is the mindset I want to carry forward into real-world junior penetration testing work.