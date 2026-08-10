# 08 - Conclusion

## Overview

Summary of the Active Directory Breaching techniques covered
throughout the module.

## Techniques Covered

### OSINT & Reconnaissance

Gathering potential usernames from public information and
identifying the organisation's username convention.

### Username Enumeration

Using Kerbrute and Kerberos behaviour to validate which
usernames exist in the domain.

### Credential Discovery

Searching exposed services such as:

- Git repositories
- Git history
- Jenkins
- CI/CD build logs
- Configuration files

### Password Spraying

Testing a single password against many validated usernames
while respecting account lockout policies.

### LDAP Passback

Redirecting a network device's LDAP connection to an
attacker-controlled listener to capture authentication
material.

### File-Based Coercion

Using a malicious file on a writable share to trigger an
NTLM authentication attempt from a Windows user.

## Attack Progression

A simplified view of the room:

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
    Further AD Enumeration / Attack Paths

## Defensive Perspective

Each technique has corresponding defensive controls:

    Secrets Management
          ↓
    Strong Password Policies
          ↓
    Device Hardening
          ↓
    Secure File Shares
          ↓
    NTLM Hardening
          ↓
    Network Segmentation
          ↓
    MFA

## Important Concepts

AD breaching is rarely a single technique.

A real engagement may combine:

- Reconnaissance
- Credential discovery
- Username enumeration
- Password spraying
- Coercion

The objective is to obtain the first valid credentials and
use them as a foothold for deeper Active Directory attacks.

## Further Techniques

The room introduces techniques that are explored in more
depth later:

- Null sessions
- Guest access
- LDAP anonymous binds
- SNMP enumeration
- PetitPotam
- PrinterBug / SpoolSample
- DFSCoerce
- NTLM relay
- LLMNR/NBT-NS poisoning
- PXE / MDT credential extraction

## Key Takeaway

The important skill is not memorising one attack.

It is understanding how different weaknesses can be combined
to move from:

    No Credentials
          ↓
    Initial Foothold
          ↓
    Valid AD Account
          ↓
    Domain Enumeration
          ↓
    Further Attack Paths