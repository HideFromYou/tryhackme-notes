# 05 - AD Authentication Enumeration

## Overview

This folder contains my notes and hands-on work from the
Active Directory Authentication Enumeration room.

The room follows AD: Basic Enumeration and focuses on
authenticated enumeration techniques that become available
once valid domain credentials have been obtained.

The main focus was learning how to enumerate Active Directory
using native Windows commands, PowerShell modules and
BloodHound, while also covering AS-REP Roasting.

## Topics Covered

- Authenticated Active Directory Enumeration
- AS-REP Roasting
- Kerberos Pre-Authentication
- Rubeus
- GetNPUsers.py
- Hashcat
- Manual Windows Enumeration
- NET commands
- PowerShell
- Microsoft ActiveDirectory Module
- PowerView
- PowerSploit
- BloodHound
- User Enumeration
- Group Enumeration
- Computer Enumeration
- Password Policy Enumeration
- Service Enumeration
- Session Enumeration
- Privilege Enumeration
- SPN Enumeration
- Active Directory Relationships
- Attack Path Discovery

## Room Structure

### 01 - Introduction

Introduction to authenticated Active Directory enumeration
and the additional information available after obtaining
valid domain credentials.

### 02 - AS-REP Roasting

Covered Kerberos accounts with pre-authentication disabled,
including enumeration and extraction of AS-REP hashes.

Tools covered:

- Rubeus
- GetNPUsers.py
- Hashcat

### 03 - Manual Enumeration

Performed enumeration using native Windows tools and
commands.

Covered:

- `whoami`
- `whoami /all`
- `systeminfo`
- `net`
- `quser`
- `tasklist`
- `sc`
- `reg`
- `schtasks`
- WMIC

Information gathered included:

- Users
- Groups
- Privileges
- Logged-on users
- Processes
- Services
- Service accounts
- Environment variables
- Registry information
- Scheduled tasks

### 04 - Enumeration With BloodHound

Used BloodHound to visualise relationships within the
Active Directory environment.

Covered:

- Users
- Groups
- Computers
- Group memberships
- Permissions
- Sessions
- Relationships
- Potential attack paths

### 05 - Enumeration With PowerShell

Explored two PowerShell-based enumeration approaches:

- Microsoft's ActiveDirectory module
- PowerView from the PowerSploit framework

ActiveDirectory commands included:

- `Get-ADUser`
- `Get-ADGroup`
- `Get-ADGroupMember`
- `Get-ADComputer`
- `Get-ADDefaultDomainPasswordPolicy`

PowerView commands included:

- `Get-DomainUser`
- `Get-DomainGroup`
- `Get-DomainComputer`
- `Get-DomainUser -AdminCount`
- `Get-DomainUser -SPN`

## Authenticated Enumeration Methodology

The overall workflow covered in the room was:

    Valid Domain Credentials
            ↓
    Manual Windows Enumeration
            ↓
    Users / Groups / Privileges
            ↓
    Sessions / Processes / Services
            ↓
    PowerShell Enumeration
            ↓
    ActiveDirectory Module
            ↓
    PowerView
            ↓
    BloodHound
            ↓
    Relationship Mapping
            ↓
    Attack Path Discovery

## AS-REP Roasting

The room also covered AS-REP Roasting against accounts where
Kerberos pre-authentication is disabled.

The basic attack flow is:

    Identify Vulnerable Account
            ↓
    Request AS-REP
            ↓
    Obtain AS-REP Hash
            ↓
    Crack Hash Offline
            ↓
    Recover Password

The room used Rubeus and `GetNPUsers.py` for enumeration and
hash extraction, followed by Hashcat for offline cracking.

## PowerShell Enumeration

The Microsoft ActiveDirectory module provides structured
access to domain objects.

Examples include:

    Get-ADUser -Filter *
    Get-ADGroup -Filter *
    Get-ADComputer -Filter *
    Get-ADDefaultDomainPasswordPolicy

PowerView provides additional Active Directory
reconnaissance capabilities.

Examples include:

    Get-DomainUser
    Get-DomainGroup
    Get-DomainComputer
    Get-DomainUser -AdminCount
    Get-DomainUser -SPN

## BloodHound

BloodHound was used to visualise relationships that exist
between Active Directory objects.

The goal is to move from individual enumeration results
towards understanding relationships and identifying
potential attack paths.

## Main Tools

    NET
    CMD
    PowerShell
    ActiveDirectory
    PowerView
    PowerSploit
    BloodHound
    Rubeus
    GetNPUsers.py
    Hashcat

## Key Takeaways

Authenticated access provides significantly more visibility
into an Active Directory environment than unauthenticated
enumeration.

The main progression is:

    Basic Enumeration
          ↓
    Valid Domain Credentials
          ↓
    Authenticated Enumeration
          ↓
    Users / Groups / Computers
          ↓
    Privileges / Sessions / Services
          ↓
    PowerShell Enumeration
          ↓
    BloodHound Relationship Mapping
          ↓
    Attack Path Discovery

## Final Takeaway

The main objective of authenticated AD enumeration is to
build a detailed understanding of the domain and identify
relationships, privileges and configurations that may lead
to further attacks.

This room demonstrated how native Windows commands,
PowerShell, PowerView and BloodHound can be combined to
move from basic authenticated access towards detailed
Active Directory reconnaissance.