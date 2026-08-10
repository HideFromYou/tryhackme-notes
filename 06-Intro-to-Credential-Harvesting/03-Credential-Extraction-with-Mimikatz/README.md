# 03 - Credential Extraction with Mimikatz

## Overview

This task focused on using Mimikatz to extract credential
material from different Windows credential stores.

The starting point was local Administrator access on a
domain-joined workstation.

## Topics Covered

- Mimikatz
- LSASS
- DPAPI
- SAM
- SYSTEM
- LSA Secrets
- Cached domain credentials
- NTLM hashes
- Windows Vault
- Credential extraction

## DPAPI Vault

List available credential vaults:

    vault::list

This can identify:

- Web Credentials
- Windows Credentials

Export credentials:

    vault::cred /export

This can expose saved application or web credentials when
the required user context and DPAPI material are available.

## SAM + SYSTEM

The SAM and SYSTEM registry hives can be exported:

    reg save HKLM\SAM C:\Users\Administrator\Desktop\SAM

    reg save HKLM\SYSTEM C:\Users\Administrator\Desktop\SYSTEM

The extracted hives can then be processed with Mimikatz:

    lsadump::sam /sam:"C:\Users\Administrator\Desktop\SAM" /system:"C:\Users\Administrator\Desktop\SYSTEM"

This can recover NTLM hashes belonging to local accounts.

## LSASS Memory

Mimikatz can access LSASS credential material after enabling
the required debug privilege.

    privilege::debug

Then:

    sekurlsa::logonpasswords

This command reads credential structures from LSASS memory.

Potential output includes:

- Usernames
- Domains
- NTLM hashes
- SHA1 hashes
- Kerberos information
- Plaintext passwords when available

## LSA Secrets

To access cached domain credentials, the token can be elevated
to SYSTEM:

    token::elevate

Then:

    lsadump::cache

This extracts cached domain logon information stored on
the workstation.

## Credential Harvesting Flow

    Local Administrator
          ↓
    Mimikatz
          ↓
    DPAPI Vault
          ↓
    SAM + SYSTEM
          ↓
    LSASS
          ↓
    LSA Secrets
          ↓
    Recovered Credentials
          ↓
    Credential Reuse / Further Access

## Important Limitation

LSASS only contains credentials from currently relevant
sessions.

A domain user's credentials may not be available in LSASS
if that user is no longer actively logged on to the
workstation.

## Key Takeaways

Mimikatz can interact with multiple Windows credential
stores.

The same compromised workstation can therefore provide
different types of credential material depending on:

- Current sessions
- User context
- Available privileges
- Credential storage mechanism