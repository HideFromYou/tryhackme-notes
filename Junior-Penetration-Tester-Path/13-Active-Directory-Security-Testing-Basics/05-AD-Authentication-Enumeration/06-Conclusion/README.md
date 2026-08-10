# 06 - Conclusion

## Overview

This room focused on authenticated Active Directory
enumeration.

It followed the AD: Basic Enumeration room and demonstrated
how having a valid domain account allows us to collect
significantly more information about the environment.

## Techniques Covered

### AS-REP Roasting

- Kerberos pre-authentication
- UF_DONT_REQUIRE_PREAUTH
- Rubeus
- GetNPUsers.py
- AS-REP hash extraction
- Hashcat
- Offline password cracking

### Manual Enumeration

- whoami
- whoami /all
- Token privileges
- System information
- Environment variables
- NET commands
- Users
- Groups
- Sessions
- Processes
- Service accounts
- Windows Registry
- Scheduled tasks

### BloodHound

- Active Directory relationships
- Users
- Groups
- Computers
- Permissions
- Graph-based enumeration
- Attack path analysis

### PowerShell Enumeration

- ActiveDirectory module
- PowerView
- User enumeration
- Group enumeration
- Computer enumeration
- Password policy
- AdminCount
- SPNs

## Overall Methodology

The room's authenticated enumeration workflow can be
summarised as:

    Valid Domain Credentials
            ↓
    Manual Windows Enumeration
            ↓
    Users / Groups / Privileges
            ↓
    Sessions / Services / Registry
            ↓
    PowerShell Enumeration
            ↓
    ActiveDirectory Module
            ↓
    PowerView
            ↓
    BloodHound
            ↓
    Identify Relationships
            ↓
    Identify Potential Attack Paths
            ↓
    Further AD Attacks

## Main Tools

    NET
    CMD
    PowerShell
    ActiveDirectory
    PowerView
    BloodHound
    Rubeus
    GetNPUsers.py
    Hashcat

## Key Takeaways

Authenticated access changes the amount and quality of
information available during Active Directory enumeration.

Instead of relying primarily on unauthenticated discovery,
we can now query the domain directly and build a much more
complete picture of:

- Users
- Groups
- Computers
- Privileges
- Sessions
- Services
- Password policies
- SPNs
- Relationships
- Potential attack paths

## Final Takeaway

The main progression of the room is:

    Basic Enumeration
          ↓
    Valid Domain Account
          ↓
    Authenticated Enumeration
          ↓
    Detailed AD Information
          ↓
    Relationship Mapping
          ↓
    Attack Path Discovery
          ↓
    Further Active Directory Attacks