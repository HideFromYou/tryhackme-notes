# 07 - Conclusion

## Overview

Summary of the Active Directory authentication concepts
covered throughout the module.

## Topics Covered

- Authentication vs Authorisation
- NTLM authentication
- Kerberos authentication
- Authentication weaknesses
- Weak password hashing
- Pass-the-Hash
- Kerberoasting
- Golden Ticket
- Windows Event IDs
- Detection
- Mitigation

## Authentication

Authentication establishes the identity of a user or machine.

## Authorisation

Authorisation determines what the authenticated identity
is allowed to access.

## NTLM

NTLM uses challenge-response authentication and has several
security weaknesses including:

- Pass-the-Hash
- NTLM Relay
- Weak cryptography
- Downgrade attacks

## Kerberos

Kerberos uses tickets for authentication.

Important components include:

- KDC
- TGT
- TGS
- SPN

## Offensive Security

The module demonstrated:

    NTLM Hash Cracking
            ↓
    Pass-the-Hash
            ↓
    Kerberoasting
            ↓
    Golden Ticket

## Defensive Security

Authentication attacks can be detected using Windows
Security Event IDs.

Important examples:

    4624
    4625
    4768
    4769
    4771

## Final Takeaway

Understanding how authentication works and where it can be
exploited is fundamental to both attacking and defending
Active Directory environments.