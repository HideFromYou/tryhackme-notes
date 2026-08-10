# 13 - Active Directory Security Testing Basics

## Overview

This module covers the fundamentals of Active Directory security testing, focusing on how attackers enumerate, compromise, and move through an Active Directory environment.

The material progresses from understanding Active Directory and its authentication mechanisms to enumeration, credential harvesting, and lateral movement.

## Topics Covered

### 01 - Active Directory Basics
- Active Directory fundamentals
- Windows domains
- Domain Controllers
- Authentication methods
- Trees, forests and trusts
- Domain creation
- Users and computers
- Group Policy
- Foreign forest trusts

### 02 - Intro to AD Authentication
- Authentication in Active Directory
- NTLM / NetNTLM
- Kerberos
- Authentication weaknesses
- Detection and mitigation

### 03 - Intro to AD Breaching
- Active Directory reconnaissance
- OSINT
- Target reconnaissance
- Credential discovery
- Username enumeration
- Password spraying
- Coercion attacks
- Mitigations

### 04 - AD Basic Enumeration
- Network mapping
- SMB enumeration
- Domain enumeration
- Password spraying

### 05 - AD Authentication Enumeration
- AS-REP Roasting
- Manual enumeration
- BloodHound
- PowerShell enumeration

### 06 - Intro to Credential Harvesting
- Windows and Active Directory credential stores
- Mimikatz
- Secretsdump
- Credential extraction
- Credential harvesting
- Mitigations

### 07 - Intro to AD Lateral Movement
- Lateral movement concepts
- Remote execution methods
- Pass-the-Hash
- Credential reuse
- Pivoting
- Proxy Challenge Room
- Forward Challenge Room

## Overall Attack Flow

```text
Active Directory Fundamentals
            ↓
Authentication
            ↓
Initial Breach
            ↓
Enumeration
            ↓
Credential Harvesting
            ↓
Credential Reuse
            ↓
Lateral Movement
            ↓
Pivoting

Objective

The objective of this module is to understand the main techniques used during Active Directory penetration testing and how individual attacks and enumeration techniques can be combined into a complete attack path.