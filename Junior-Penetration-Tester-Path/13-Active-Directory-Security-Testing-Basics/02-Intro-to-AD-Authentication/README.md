# 02 - Intro to AD Authentication

## Overview

This folder contains my notes and hands-on work from the
TryHackMe Active Directory Authentication module.

The module focuses on how authentication works in Active
Directory, the authentication protocols used by Windows
domains, common weaknesses in these protocols, practical
authentication attacks, and defensive detection and mitigation.

## Topics Covered

- Authentication
- Authorisation
- Authentication Material
- NTLM / NetNTLM
- Kerberos
- Key Distribution Center (KDC)
- Ticket Granting Tickets (TGT)
- Ticket Granting Service (TGS)
- Service Principal Names (SPNs)
- Kerberos Credential Cache
- KRB5CCNAME
- NTLM Hash Cracking
- Pass-the-Hash
- NTLM Relay
- Kerberoasting
- AS-REP Roasting
- Pass-the-Ticket
- Overpass-the-Hash
- Golden Ticket
- Silver Ticket
- Password Spraying
- Windows Security Event IDs
- Authentication Attack Detection
- Authentication Attack Mitigation

## Module Structure

### 01 - Introduction

Introduction to authentication in Active Directory and the
difference between authentication and authorisation.

### 02 - Authentication in AD

Explored authentication material, authentication protocols
and how authentication and authorisation work together.

### 03 - NetNTLM Authentication

Studied the NTLM challenge-response authentication process
and its security weaknesses.

### 04 - Kerberos Authentication

Studied Kerberos authentication, including KDC, TGT, TGS,
SPNs and Kerberos credential caches.

### 05 - Weaknesses in AD Authentication

Explored common weaknesses in NTLM and Kerberos and performed
hands-on demonstrations of:

- NTLM hash cracking
- Pass-the-Hash
- Kerberoasting
- Golden Ticket

### 06 - Detections & Mitigations

Studied Windows Security Event IDs used to detect
authentication attacks and the corresponding mitigations.

### 07 - Conclusion

Reviewed the authentication concepts, attacks, detection
methods and defensive techniques covered in the module.

## Authentication vs Authorisation

Authentication answers:

    "Who are you?"

Authorisation answers:

    "What are you allowed to access?"

Authentication must occur before authorisation can determine
what resources the identity is permitted to access.

## Authentication Protocols

The two core authentication protocols covered were:

    NTLM
    Kerberos

### NTLM

NTLM uses a challenge-response authentication mechanism.

Important weaknesses include:

- Pass-the-Hash
- NTLM Relay
- Weak cryptography
- Downgrade attacks
- Lack of mutual authentication

### Kerberos

Kerberos uses a ticket-based authentication mechanism.

Important components include:

- KDC
- TGT
- TGS
- SPN

## Authentication Attacks

The practical attacks covered in the module included:

    NTLM Hash Cracking
            ↓
    Pass-the-Hash
            ↓
    Kerberoasting
            ↓
    Golden Ticket

Other authentication weaknesses discussed included:

- AS-REP Roasting
- Pass-the-Ticket
- Overpass-the-Hash
- Silver Ticket
- Password Spraying
- Weak passwords
- Misconfigured delegation
- Stale credentials

## Detection

Important Windows Security Event IDs covered:

| Event ID | Description |
|---|---|
| 4624 | Successful logon |
| 4625 | Failed logon |
| 4768 | Kerberos TGT requested |
| 4769 | Kerberos service ticket requested |
| 4771 | Kerberos pre-authentication failed |

## Mitigation

Defensive techniques covered included:

- Protecting privileged accounts
- Disabling NTLM where Kerberos is available
- Enforcing SMB signing
- Enabling Extended Protection for Authentication (EPA)
- Using strong service-account passwords
- Using Group Managed Service Accounts (gMSA)
- Protecting the KRBTGT account
- Resetting KRBTGT credentials after suspected compromise
- Configuring account lockout policies
- Monitoring authentication-related Event IDs

## Key Takeaways

Active Directory authentication is based primarily around
NTLM and Kerberos.

Understanding how these protocols authenticate users,
how authentication material can be abused, and what traces
the attacks leave in Windows logs is fundamental to both
offensive and defensive Active Directory security.

The module connects the concepts of:

    Authentication
          ↓
    Authentication Material
          ↓
    NTLM / Kerberos
          ↓
    Authentication Weaknesses
          ↓
    Credential / Ticket Abuse
          ↓
    Detection & Mitigation

## Purpose

These notes document my learning and hands-on practice with
Active Directory authentication as part of my cybersecurity
and penetration testing training.