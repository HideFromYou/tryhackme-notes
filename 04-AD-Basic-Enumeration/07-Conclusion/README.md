# 07 - Conclusion

## Overview

This task brought together the unauthenticated Active Directory
enumeration techniques covered throughout the room.

The objective was to move from basic network discovery to
identifying valid domain users and eventually testing
passwords against those accounts.

## Techniques Covered

### Network Mapping

- Host discovery
- fping
- Nmap
- Port scanning
- Service detection
- Domain Controller identification

### SMB Enumeration

- SMB discovery
- Anonymous SMB access
- Null sessions
- smbclient
- smbmap
- enum4linux
- SMB share enumeration
- Share permissions
- File retrieval

### Domain Enumeration

- LDAP anonymous bind
- ldapsearch
- enum4linux-ng
- RPC null sessions
- rpcclient
- RID cycling
- Kerbrute
- Username enumeration

### Password Spraying

- Password policy enumeration
- Account lockout awareness
- CrackMapExec
- SMB password spraying
- Credential validation

## Overall Enumeration Methodology

The methodology followed throughout the room was:

    Network Discovery
          ↓
    Identify Live Hosts
          ↓
    Identify Services
          ↓
    Identify Domain Controller
          ↓
    SMB Enumeration
          ↓
    LDAP / RPC Enumeration
          ↓
    User Enumeration
          ↓
    Kerberos Username Validation
          ↓
    Password Policy Enumeration
          ↓
    Password Spraying
          ↓
    Valid AD Credentials

## Main Tools

The main tools used throughout the room were:

    fping
    Nmap
    smbclient
    smbmap
    enum4linux
    enum4linux-ng
    ldapsearch
    rpcclient
    Kerbrute
    CrackMapExec

## Key Takeaways

Active Directory can expose a significant amount of
information before authentication.

The important progression is:

    Network
      ↓
    Services
      ↓
    SMB
      ↓
    Domain Information
      ↓
    Users
      ↓
    Password Policy
      ↓
    Password Spray
      ↓
    Initial Credentials

Each enumeration step provides information that can be
used to guide the next stage of the assessment.

## Final Takeaway

The goal of basic AD enumeration is to understand the
environment before attempting more advanced attacks.

By combining network discovery, SMB enumeration, domain
enumeration and password spraying, an attacker can potentially
move from an unauthenticated position to obtaining valid
Active Directory credentials.