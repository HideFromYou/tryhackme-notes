# 01 - Introduction

## Overview

This task introduces credential harvesting in Windows and
Active Directory environments.

The focus is on understanding where credentials are stored,
why Windows stores them in different locations, and how
credential material can be recovered after gaining access
to a compromised system.

## Topics Covered

- Credential harvesting
- Windows credential stores
- Active Directory credential stores
- Credential material
- Password hashes
- Kerberos tickets
- Cached credentials
- LSASS
- SAM
- SYSTEM
- LSA Secrets
- DPAPI
- NTDS.dit

## Credential Harvesting

Windows and Active Directory store credential material in
multiple locations depending on how the credentials are
used.

From a penetration testing perspective, these locations
represent different opportunities for credential collection.

## Main Credential Stores

    LSASS Memory
        ↓
    SAM + SYSTEM
        ↓
    LSA Secrets
        ↓
    DPAPI Vault
        ↓
    NTDS.dit

Each store contains different types of credential material
and requires different privileges and extraction techniques.

## Attack Progression

The room starts from local Administrator access and
demonstrates how credentials can be harvested from a
compromised Windows workstation.

The recovered credentials can then be reused to move
through the Active Directory environment.

## Key Takeaway

Credential harvesting is not limited to recovering a
plaintext password.

An attacker may obtain:

- NTLM hashes
- Kerberos tickets
- Cached domain credentials
- Service credentials
- Application credentials
- DPAPI-protected secrets
- Domain credential material

Understanding where Windows stores each type of credential
is essential for both penetration testing and defense.