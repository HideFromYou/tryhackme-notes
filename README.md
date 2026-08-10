
# TryHackMe Notes

A structured collection of my notes, walkthroughs, and hands-on practice while studying cybersecurity through **TryHackMe**.

This repository documents my learning journey across official learning paths and Capture The Flag (CTF) rooms, with a primary focus on offensive security, penetration testing, and practical lab exercises.

## Repository Structure

```text
tryhackme-notes/
│
├── Junior-Penetration-Tester-Path/
│   ├── Intro-Web-Hacking/
│   ├── 01-Penetration-Testing-Foundations/
│   ├── 02-Network-Reconnaissance/
│   ├── ...
│   └── 18-PT1-Certification/
│
└── CTF/
    └── TryHackMe/
```

## Junior Penetration Tester Path

This section contains my notes from the **TryHackMe Junior Penetration Tester Path**.

The content follows the learning path structure and includes:

* Personal notes
* Commands and techniques
* Challenge solutions
* Practical examples
* Key takeaways from each lesson

## CTF

The CTF section contains write-ups and walkthrough notes from TryHackMe rooms completed outside the official learning path.

These rooms are used to practice real-world enumeration, exploitation, privilege escalation, and penetration testing methodology.

## Goals

* Document my cybersecurity learning journey.
* Build a structured penetration testing knowledge base.
* Organize notes for future revision.
* Track completed learning paths and CTF rooms.
* Continuously improve practical offensive security skills.

## Disclaimer

This repository is intended for educational purposes only.

All notes are based on my personal learning experience while studying on the TryHackMe platform. The content is not affiliated with or endorsed by TryHackMe.
=======
# Active Directory - Penetration Testing Notes

## Overview

This repository contains my notes and hands-on work covering
the fundamentals of Active Directory penetration testing.

The material progresses from basic Active Directory concepts
and authentication, through unauthenticated and authenticated
enumeration, credential harvesting and finally lateral
movement.

The overall goal is to understand how an attacker can progress
through an Active Directory environment from initial
reconnaissance to obtaining credentials, moving between hosts
and reaching high-value systems.

## Modules

### 01 - Active Directory Basics

Introduction to the fundamentals of Active Directory and
its core components.

Topics include:

- Active Directory structure
- Domains
- Domain Controllers
- Users
- Groups
- Computers
- Organizational Units
- Group Policy
- Authentication
- Kerberos
- LDAP
- SMB
- Active Directory terminology

---

### 02 - Intro to AD Authentication

Introduction to authentication within an Active Directory
environment.

Topics include:

- Authentication
- Authorization
- Kerberos
- NTLM
- LDAP
- Domain authentication
- Authentication workflows
- AD authentication concepts

---

### 03 - Intro to AD Breaching

Focused on obtaining the first valid Active Directory
credentials from an unauthenticated position.

Topics include:

- OSINT
- Target reconnaissance
- Username enumeration
- Kerbrute
- DNS enumeration
- Credential discovery
- Git repositories
- Jenkins
- Password spraying
- NetExec
- LDAP Passback
- File-based coercion
- Responder
- NTLMv2
- Hashcat

Main progression:

    OSINT
      ↓
    Username Enumeration
      ↓
    Credential Discovery
      ↓
    Password Spraying
      ↓
    Authentication Coercion
      ↓
    Valid AD Credentials

---

### 04 - AD Basic Enumeration

Focused on unauthenticated enumeration of an Active
Directory environment.

Topics include:

- Network mapping
- Host discovery
- fping
- Nmap
- SMB enumeration
- smbclient
- smbmap
- enum4linux
- LDAP
- ldapsearch
- RPC
- rpcclient
- RID cycling
- Kerbrute
- Password policy enumeration
- Password spraying
- CrackMapExec

Main progression:

    Network Discovery
          ↓
    Service Enumeration
          ↓
    Domain Controller
          ↓
    SMB Enumeration
          ↓
    Domain Enumeration
          ↓
    User Enumeration
          ↓
    Password Policy
          ↓
    Password Spraying

---

### 05 - AD Authentication Enumeration

Focused on authenticated Active Directory enumeration
after obtaining valid domain credentials.

Topics include:

- Authenticated enumeration
- AS-REP Roasting
- Kerberos pre-authentication
- Rubeus
- GetNPUsers.py
- Hashcat
- Manual Windows enumeration
- NET commands
- PowerShell
- ActiveDirectory module
- PowerView
- BloodHound
- Users
- Groups
- Computers
- Privileges
- Sessions
- Services
- SPNs
- Attack path discovery

Main progression:

    Valid Domain Credentials
          ↓
    Manual Enumeration
          ↓
    PowerShell Enumeration
          ↓
    PowerView
          ↓
    BloodHound
          ↓
    Relationship Mapping
          ↓
    Attack Path Discovery

---

### 06 - Intro to Credential Harvesting

Focused on identifying and extracting credential material
from Windows and Active Directory systems.

Topics include:

- Windows credential stores
- LSASS
- SAM
- SYSTEM
- LSA Secrets
- DPAPI
- Windows Credential Vault
- NTDS.dit
- NTLM hashes
- Kerberos credentials
- Cached domain credentials
- Mimikatz
- secretsdump.py
- DCC2 / MSCacheV2
- Hash cracking
- DCSync
- Pass-the-Hash
- PsExec

Main progression:

    Local Administrator
          ↓
    Credential Harvesting
          ↓
    Local / Cached Credentials
          ↓
    Credential Cracking
          ↓
    Domain Access
          ↓
    Domain Credential Extraction
          ↓
    Pass-the-Hash
          ↓
    Further Access

---

### 07 - Intro to AD Lateral Movement

Focused on moving from one compromised host to another
inside an Active Directory environment.

Topics include:

- Lateral movement
- Remote execution
- PsExec
- Evil-WinRM
- WinRM
- WMI
- DCOM
- SMBExec
- AtExec
- Credential reuse
- Pass-the-Hash
- NTLM hashes
- Pivoting
- SSH tunnelling
- SOCKS proxies
- ProxyChains
- NetExec
- Impacket
- Network segmentation
- Windows LAPS
- SMB signing
- NTLM restrictions
- Privileged Access Workstations

Main progression:

    Compromised Host
          ↓
    Remote Execution
          ↓
    Credential Harvesting
          ↓
    Pass-the-Hash
          ↓
    Further Lateral Movement
          ↓
    Pivoting
          ↓
    Restricted Network
          ↓
    Domain Controller

## Overall Attack Chain

The seven modules build progressively on each other.

The complete methodology can be represented as:

    Active Directory Fundamentals
              ↓
    Authentication
              ↓
    Initial AD Breach
              ↓
    Unauthenticated Enumeration
              ↓
    Authenticated Enumeration
              ↓
    Credential Harvesting
              ↓
    Lateral Movement
              ↓
    Higher-Value Systems
              ↓
    Domain Controller

## Main Tools

Throughout these modules, the main tools covered include:

    Nmap
    fping
    smbclient
    smbmap
    enum4linux
    enum4linux-ng
    ldapsearch
    rpcclient
    Kerbrute
    NetExec
    CrackMapExec
    Mimikatz
    secretsdump.py
    Rubeus
    Hashcat
    John the Ripper
    BloodHound
    PowerView
    Evil-WinRM
    Impacket
    PsExec
    SSH
    ProxyChains

## Core Concepts

The main concepts developed throughout the modules are:

### Enumeration

Understanding the environment before attacking it.

    Hosts
      ↓
    Services
      ↓
    Users
      ↓
    Groups
      ↓
    Computers
      ↓
    Relationships
      ↓
    Attack Paths

### Credentials

Understanding where authentication material exists and
how it can be obtained, cracked or reused.

    Passwords
    NTLM Hashes
    Kerberos Tickets
    Cached Credentials
    Service Credentials
    DPAPI Secrets

### Lateral Movement

Using valid authentication material to move between systems.

    Credentials
          ↓
    Authentication
          ↓
    Remote Execution
          ↓
    New Host
          ↓
    More Credentials

### Pivoting

Using a compromised system as a bridge to reach restricted
network segments.

    Attacker
       ↓
    Pivot Host
       ↓
    Internal Network
       ↓
    Restricted Target

## Defensive Perspective

The material also introduces defensive controls that can
break different stages of the attack chain.

Important controls include:

- Strong password policies
- Secrets management
- Least privilege
- Windows LAPS
- Credential Guard
- SMB signing
- NTLM restrictions
- Network segmentation
- Host firewall rules
- Privileged Access Workstations
- MFA
- Monitoring and detection

## Final Takeaway

The main lesson across these modules is that an Active
Directory compromise is rarely the result of one isolated
technique.

Instead, attackers combine multiple stages:

    Reconnaissance
          ↓
    Enumeration
          ↓
    Credential Discovery
          ↓
    Authentication
          ↓
    Credential Harvesting
          ↓
    Credential Reuse
          ↓
    Lateral Movement
          ↓
    Pivoting
          ↓
    Higher Privileges
          ↓
    Domain Controller

Understanding this chain is essential for approaching
Active Directory penetration testing as a complete process
rather than as a collection of unrelated tools and attacks.
>>>>>>> a1ab9a5 (Add AD penetration testing notes 01-07)
