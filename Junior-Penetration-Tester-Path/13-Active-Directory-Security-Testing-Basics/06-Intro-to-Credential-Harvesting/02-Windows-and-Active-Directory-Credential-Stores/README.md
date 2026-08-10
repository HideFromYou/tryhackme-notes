# 02 - Windows and Active Directory Credential Stores

## Overview

This task explored the different locations where Windows and
Active Directory store credential material.

The focus was on understanding what each credential store
contains, why it exists, how it can be accessed and which
tools can be used to extract its contents.

## Topics Covered

- LSASS Memory
- SAM
- SYSTEM
- LSA Secrets
- DPAPI Vault
- NTDS.dit
- NTLM hashes
- Kerberos tickets
- Cached domain credentials
- Local account hashes
- Service credentials

## LSASS Memory

The Local Security Authority Subsystem Service (LSASS)
manages Windows authentication.

It can hold sensitive credential material in memory,
including:

- NTLM hashes
- LM hashes
- Kerberos tickets
- TGTs
- Service tickets
- Sometimes plaintext credentials

Because LSASS contains live authentication material, it is
a high-value target for credential theft.

Access to LSASS memory generally requires elevated
privileges.

## SAM + SYSTEM

The Security Accounts Manager (SAM) stores password hashes
for local Windows accounts.

The SAM database contains local account information,
including local administrator credentials.

The hashes are protected using a key derived from the
SYSTEM hive.

Relevant locations:

    C:\Windows\System32\config\SAM
    C:\Windows\System32\config\SYSTEM

Both hives are required to recover the local account hashes.

## LSA Secrets

LSA Secrets are stored under:

    HKLM\SECURITY\Policy\Secrets

They may contain:

- Cached domain credentials
- Service account credentials
- Scheduled task passwords
- Other sensitive secrets

Access generally requires SYSTEM-level privileges.

## DPAPI Vault

The Data Protection API (DPAPI) protects application secrets
for individual Windows users.

It can protect credentials such as:

- Saved Wi-Fi passwords
- Browser credentials
- RDP credentials
- Application secrets

DPAPI master keys are stored under:

    %APPDATA%\Microsoft\Protect

Access to the required master key and user context can allow
the protected secrets to be decrypted.

## NTDS.dit

NTDS.dit is the Active Directory database located on
Domain Controllers.

It contains information including:

- Domain users
- Computer accounts
- Service principals
- NTLM password hashes
- Kerberos key material

Location:

    C:\Windows\NTDS\ntds.dit

Because it represents the authentication database for the
domain, it is one of the highest-value credential stores
in an AD environment.

## Credential Store Summary

| Store | Main Contents | Typical Tool |
|---|---|---|
| LSASS | NTLM hashes, Kerberos tickets, credentials | Mimikatz |
| SAM + SYSTEM | Local account hashes | Mimikatz |
| LSA Secrets | Cached/service credentials | Secretsdump / Mimikatz |
| DPAPI | Application and saved credentials | Mimikatz |
| NTDS.dit | Domain credentials and Kerberos keys | Secretsdump |

## Main Tools

    Mimikatz
    secretsdump.py

## Key Takeaway

Different credential stores require different extraction
methods.

Understanding the storage mechanism is the first step toward
choosing the appropriate credential harvesting technique.