# 06 - Intro to Credential Harvesting

## Overview

This folder contains my notes and hands-on work from the
TryHackMe Introduction to Credential Harvesting room.

The room focuses on identifying where Windows and Active
Directory store credential material, extracting credentials
from a compromised Windows system, and using the recovered
credentials to move further through the Active Directory
environment.

The practical path starts with local Administrator access
on a domain-joined workstation and progresses through
credential harvesting techniques until Domain Administrator
access is obtained.

## Topics Covered

- Windows Credential Stores
- Active Directory Credential Stores
- LSASS Memory
- SAM
- SYSTEM
- LSA Secrets
- DPAPI
- Windows Credential Vault
- NTDS.dit
- NTLM Hashes
- Kerberos Credentials
- Cached Domain Credentials
- Mimikatz
- secretsdump.py
- MSCacheV2 / DCC2
- Hash Cracking
- Pass-the-Hash
- PsExec
- DCSync / DRSUAPI
- Windows LAPS
- Least Privilege
- SMB Signing
- NTLM Restrictions
- Credential Guard
- Network Segmentation
- Privileged Access Workstations
- Windows Event IDs
- Sysmon

## Room Structure

### 01 - Introduction

Introduction to credential harvesting and the different
locations where Windows and Active Directory store
credential material.

### 02 - Windows and Active Directory Credential Stores

Covered the main credential stores:

- LSASS
- SAM + SYSTEM
- LSA Secrets
- DPAPI Vault
- NTDS.dit

Each store contains different types of credentials and
requires different access methods.

### 03 - Credential Extraction with Mimikatz

Used Mimikatz to extract credentials from:

- DPAPI Vault
- SAM + SYSTEM
- LSASS
- LSA Secrets
- Cached domain credentials

The task demonstrated how local Administrator access can
provide access to multiple credential stores.

### 04 - Credential Harvesting with Secretsdump

Used `secretsdump.py` remotely to extract:

- Local SAM hashes
- Cached domain credentials
- DCC2 / MSCacheV2 hashes
- Domain NTLM hashes
- Kerberos keys

The task then demonstrated offline cracking, Pass-the-Hash
and remote execution with PsExec.

### 05 - Conclusion

Reviewed how credentials can be collected from different
locations and reused to move through the Active Directory
environment.

### 06 - Mitigations

Covered defensive controls designed to prevent credential
harvesting and limit lateral movement.

## Credential Stores

The main credential stores covered were:

    LSASS Memory
          ↓
    SAM + SYSTEM
          ↓
    LSA Secrets
          ↓
    DPAPI Vault
          ↓
    NTDS.dit

### LSASS

Can contain live authentication material such as:

- NTLM hashes
- Kerberos tickets
- Sometimes plaintext credentials

### SAM + SYSTEM

The SAM stores local account password hashes.

The SYSTEM hive contains the key material required to
decrypt the SAM database.

### LSA Secrets

Can contain:

- Cached domain credentials
- Service credentials
- Scheduled task credentials
- Other sensitive secrets

### DPAPI

Protects application credentials such as:

- RDP credentials
- Browser credentials
- Wi-Fi credentials
- Other application secrets

### NTDS.dit

The Active Directory database on Domain Controllers.

It contains domain authentication information including:

- Domain accounts
- NTLM hashes
- Kerberos key material
- Computer accounts
- Service principals

## Mimikatz

Mimikatz was used to interact with multiple Windows
credential stores.

Important commands covered:

    vault::list
    vault::cred /export

    lsadump::sam

    privilege::debug
    sekurlsa::logonpasswords

    token::elevate
    lsadump::cache

## Secretsdump

`secretsdump.py` was used for remote credential extraction
through Windows services and DCE/RPC.

The practical workflow progressed from local Administrator
credentials to cached domain credentials and eventually
domain-wide credential extraction.

## DCC2 / MSCacheV2

Cached domain credentials can be represented as DCC2 hashes.

These hashes cannot be directly used for Pass-the-Hash.

Instead, they can be cracked offline using tools such as:

    John the Ripper
    Hashcat

## DCSync / Domain Credential Extraction

With sufficient privileges, `secretsdump.py` can use the
DRSUAPI method to extract credentials from the Domain
Controller.

The resulting information can include:

- NTLM hashes
- Kerberos keys
- Domain user credentials
- Computer account credentials
- krbtgt material

## Pass-the-Hash

Once a Domain Administrator NTLM hash was obtained, the
plaintext password was no longer required for authentication.

The hash could be reused for Pass-the-Hash authentication.

PsExec was then used to obtain a SYSTEM shell on the
Domain Controller.

## Overall Attack Chain

The main practical progression was:

    Local Administrator
          ↓
    Credential Harvesting
          ↓
    SAM / LSASS / LSA / DPAPI
          ↓
    Cached Domain Credentials
          ↓
    Offline Cracking
          ↓
    Domain User Access
          ↓
    Domain Administrator
          ↓
    NTDS.dit / DCSync
          ↓
    Domain NTLM Hashes
          ↓
    Pass-the-Hash
          ↓
    SYSTEM on Domain Controller

## Mitigations

The defensive techniques covered include:

- Windows LAPS
- Least Privilege
- Restricting Local Administrator Rights
- SMB Signing
- Restricting NTLM
- Credential Guard
- Host Firewall Rules
- Network Segmentation
- Privileged Access Workstations
- Monitoring and Detection

## Detection

Important Windows Event IDs covered:

| Event ID | Description |
|---:|---|
| 4624 Type 3 | Network logon |
| 4624 Type 10 | Remote interactive logon |
| 4648 | Explicit credential use |
| 7045 | New service installed |
| 4698 | Scheduled task created |
| 4688 | Process creation |

Sysmon was also covered, particularly:

    Event ID 1
    Process creation

    Event ID 10
    Process access

Event ID 10 can help identify suspicious access to
`lsass.exe`.

## Key Takeaways

Credentials can exist in many different locations across
Windows and Active Directory.

A compromised workstation can therefore become a source of
valuable credential material even when the target user's
plaintext password is not immediately available.

The important skill is understanding:

    Where credentials are stored
          ↓
    What type of credential material exists
          ↓
    What privileges are required
          ↓
    Which tool can extract it
          ↓
    Whether it can be cracked or reused
          ↓
    How it can lead to further access

## Final Takeaway

The room demonstrates how credential harvesting can turn
local Administrator access into domain-wide compromise.

The progression from Windows credential stores to Mimikatz,
secretsdump, credential cracking, DCSync and Pass-the-Hash
shows how individual credential weaknesses can be chained
together to eventually reach Domain Administrator access.