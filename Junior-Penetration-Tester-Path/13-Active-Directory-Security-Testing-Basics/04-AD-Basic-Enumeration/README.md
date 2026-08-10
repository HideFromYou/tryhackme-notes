# 04 - AD Basic Enumeration

## Overview

This folder contains my notes and hands-on work from the
Active Directory Basic Enumeration module.

The module focuses on performing unauthenticated enumeration
against an Active Directory environment, starting from basic
network discovery and progressing towards identifying valid
domain users and testing potential credentials.

## Topics Covered

- Network Mapping
- Host Discovery
- ICMP
- fping
- Nmap
- Port Scanning
- Service Enumeration
- Domain Controller Identification
- SMB Enumeration
- Anonymous SMB Access
- Null Sessions
- smbclient
- smbmap
- enum4linux
- LDAP
- ldapsearch
- Anonymous LDAP Bind
- RPC
- rpcclient
- RID Cycling
- enum4linux-ng
- Kerbrute
- Username Enumeration
- Password Policy Enumeration
- Password Spraying
- CrackMapExec
- Account Lockout

## Module Structure

### 01 - Introduction

Introduction to unauthenticated Active Directory
enumeration and the overall methodology used throughout
the module.

### 02 - Mapping Out the Network

Mapped the target network to identify live hosts, open ports,
running services and the Domain Controller.

Main tools:

- fping
- Nmap

### 03 - Network Enumeration With SMB

Enumerated SMB services and shares without valid credentials.

Main tools:

- Nmap
- smbclient
- smbmap
- enum4linux
- enum4linux-ng
- Impacket
- CrackMapExec

Covered:

- Anonymous SMB access
- Null sessions
- Share enumeration
- Share permissions
- File retrieval

### 04 - Domain Enumeration

Enumerated Active Directory information through LDAP, RPC
and Kerberos.

Covered:

- Anonymous LDAP bind
- LDAP user enumeration
- RPC null sessions
- RID cycling
- Domain user enumeration
- Kerbrute username validation

Main tools:

- ldapsearch
- enum4linux-ng
- rpcclient
- Kerbrute

### 05 - Password Spraying

Performed password spraying against discovered Active
Directory users.

Before spraying, the domain password policy was
enumerated to understand:

- Minimum password length
- Password complexity
- Password history
- Account lockout threshold
- Lockout duration
- Reset counter

Main tools:

- rpcclient
- CrackMapExec

## Enumeration Methodology

The overall methodology covered in the module was:

    Network Discovery
          ↓
    Live Hosts
          ↓
    Port & Service Enumeration
          ↓
    Domain Controller Identification
          ↓
    SMB Enumeration
          ↓
    LDAP / RPC Enumeration
          ↓
    Domain User Enumeration
          ↓
    Kerberos Username Validation
          ↓
    Password Policy Enumeration
          ↓
    Password Spraying
          ↓
    Valid AD Credentials

## Network Enumeration

The first stage was identifying live hosts within the
target subnet.

Tools used:

    fping
    Nmap

After identifying live systems, we enumerated important
Active Directory services such as:

    Kerberos
    LDAP
    SMB
    MS-RPC

The combination of these services can help identify the
Domain Controller.

## SMB Enumeration

SMB was investigated for accessible shares and useful
information.

The main workflow was:

    Discover SMB
        ↓
    Enumerate Shares
        ↓
    Identify Permissions
        ↓
    Access Anonymous Shares
        ↓
    Download Interesting Files
        ↓
    Search for Sensitive Information

## Domain Enumeration

After identifying the Domain Controller, different protocols
were used to enumerate domain information.

### LDAP

Tested whether anonymous LDAP queries were allowed.

### RPC

Tested for anonymous RPC access through null sessions.

### RID Cycling

Queried Windows Security Identifier RIDs to identify
potential domain users.

### Kerbrute

Used Kerberos username enumeration to validate discovered
usernames.

## Password Spraying

After obtaining a list of valid users, the next step was
password spraying.

The process was:

    Valid User List
          ↓
    Password Policy
          ↓
    Candidate Passwords
          ↓
    Password Spray
          ↓
    Valid Credentials

A key consideration was the account lockout policy.

The goal of password spraying is to minimise failed
authentication attempts against each individual account.

## Main Tools

The module provided hands-on experience with:

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

Unauthenticated Active Directory enumeration can reveal
significant information about an environment before valid
credentials are obtained.

The important progression is:

    Network
      ↓
    Services
      ↓
    SMB Shares
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

Each stage provides information that can be used to guide
the next stage of the assessment.

## Final Takeaway

The purpose of basic AD enumeration is to build an accurate
picture of the environment before moving to more advanced
Active Directory attacks.

The combination of network discovery, SMB enumeration,
LDAP/RPC enumeration, Kerberos username validation and
password spraying can potentially move an attacker from an
unauthenticated position to obtaining valid Active Directory
credentials.