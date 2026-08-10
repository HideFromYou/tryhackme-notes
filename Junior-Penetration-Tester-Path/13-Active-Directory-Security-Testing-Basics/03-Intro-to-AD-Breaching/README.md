# 03 - Intro to AD Breaching

## Overview

This folder contains my notes and hands-on work from the
TryHackMe Introduction to AD Breaching module.

The module focuses on how an attacker can obtain the first
valid Active Directory credentials through reconnaissance,
credential discovery, password spraying and authentication
coercion.

The main idea is that AD breaching is rarely based on a
single technique. Different pieces of information and
misconfigurations can be combined to obtain an initial
foothold in the domain.

## Topics Covered

- Active Directory Breaching
- Initial Access
- OSINT
- Target Reconnaissance
- Username Enumeration
- Kerberos Enumeration
- Kerbrute
- DNS Enumeration
- Credential Discovery
- Git Repositories
- Git History
- Jenkins
- CI/CD Logs
- Password Spraying
- NetExec
- Account Lockout Policies
- LDAP Passback
- Network Printers
- File-Based Coercion
- NTLMv2
- Responder
- Hashcat
- Mitigations
- NTLM Hardening
- SMB Signing
- Network Segmentation
- MFA

## Module Structure

### 01 - Introduction

Introduction to AD breaching and the objective of obtaining
the first valid domain credentials.

### 02 - Active Directory Breaching

Explored the main AD attack surface and the difference
between unauthenticated and authenticated starting positions.

### 03 - OSINT and Target Reconnaissance

Used public information to identify potential usernames and
then validated them against the domain using Kerberos
username enumeration.

### 04 - Credential Discovery

Explored exposed credentials in:

- Git repositories
- Git commit history
- Configuration files
- Jenkins
- CI/CD build logs
- Environment variables

### 05 - Username Enumeration and Password Spraying

Validated usernames and performed password spraying while
taking account lockout policies into consideration.

### 06 - Coercion Attacks

Covered:

- LDAP Passback
- File-Based Coercion
- NTLMv2 capture
- Responder
- Offline password cracking

### 07 - Mitigations

Covered defensive controls for the techniques used throughout
the room.

### 08 - Conclusion

Reviewed the complete AD breaching methodology and the
different techniques that can be combined during an
engagement.

## AD Breaching Methodology

The overall workflow covered in the room can be represented
as:

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
      ↓
    Further AD Enumeration
      ↓
    Additional Attack Paths

## OSINT & Reconnaissance

Potential usernames can be gathered from public sources such
as:

- LinkedIn
- GitHub
- GitLab
- Corporate websites
- Job listings
- Public data breaches

After identifying the organisation's username convention,
potential usernames can be validated against the domain.

Kerbrute was used for this purpose.

## Credential Discovery

Credentials may be exposed in:

    Git repositories
    Git history
    Configuration files
    Jenkins
    CI/CD build logs

A particularly important concept is that removing a secret
from the latest Git commit does not remove it from the
repository's history.

## Password Spraying

Password spraying tests one password against multiple
accounts.

    One password
          ↓
    Multiple usernames

This differs from traditional brute-forcing:

    One account
          ↓
    Multiple passwords

Password spraying must take account lockout policies into
consideration.

NetExec was used to perform SMB password spraying.

## Authentication Coercion

The room covered two beginner-friendly coercion techniques.

### LDAP Passback

A misconfigured network device can be manipulated to send
its LDAP authentication to an attacker-controlled listener.

If plaintext LDAP is used, credentials may be captured in
plaintext.

### File-Based Coercion

A malicious `.url` file can cause Windows Explorer to attempt
SMB authentication to an attacker-controlled system.

The resulting NTLMv2 authentication material can then be
captured with Responder and potentially cracked offline.

## Defensive Controls

The main mitigations covered include:

### Secrets Management

- Use dedicated secrets vaults
- Scan repositories for exposed secrets
- Audit Git history
- Rotate exposed credentials
- Protect CI/CD logs

### Password Security

- Use long passwords
- Block common passwords
- Avoid organisation-wide default passwords
- Configure account lockout policies
- Monitor distributed authentication failures

### Device Hardening

- Change default device credentials
- Use LDAPS instead of plaintext LDAP
- Restrict device administration interfaces
- Use dedicated low-privilege service accounts
- Include network devices in vulnerability management

### File Share Security

- Apply least privilege
- Restrict write permissions
- Monitor suspicious file types
- Monitor unusual SMB authentication activity

### NTLM Hardening

- Disable NTLMv1
- Enforce NTLMv2
- Enforce SMB signing
- Block unnecessary outbound SMB traffic
- Plan for NTLM deprecation

### Network Security

- Segment management interfaces
- Restrict internal services
- Use dedicated management networks
- Enable MFA on critical services

## Key Takeaways

The main lesson from this module is that Active Directory
breaching is a chain of techniques rather than a single
exploit.

A typical progression can be:

    Public Information
          ↓
    Potential Usernames
          ↓
    Validated Users
          ↓
    Exposed Credentials / Weak Passwords
          ↓
    Password Spraying or Coercion
          ↓
    Initial AD Credentials
          ↓
    Further Enumeration & Attacks

Each technique provides a different opportunity to obtain
the initial foothold.

The ability to recognise these opportunities and combine
them is an important part of Active Directory penetration
testing.

## Hands-On Techniques

During the module I worked with:

- Kerbrute
- NetExec
- Responder
- Netcat
- Hashcat
- SMB
- LDAP
- Kerberos
- Git
- Jenkins

## Final Takeaway

The objective of AD breaching is not simply to "find a
password".

The objective is to understand the environment, identify
weaknesses, combine available information and techniques, and
turn those weaknesses into valid access to the Active
Directory environment.