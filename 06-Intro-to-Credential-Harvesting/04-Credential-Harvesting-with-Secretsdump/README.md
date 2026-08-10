# 04 - Credential Harvesting with Secretsdump

## Overview

This task focused on remote credential harvesting using
secretsdump.py from the Impacket toolkit.

Unlike local credential extraction, secretsdump can retrieve
credential material remotely through native Windows services.

## Topics Covered

- Impacket
- secretsdump.py
- SMB
- DCE/RPC
- SAM hashes
- LSA Secrets
- MSCacheV2
- DCC2
- NTDS.dit
- DRSUAPI
- DCSync
- NTLM hashes
- Pass-the-Hash
- PsExec

## Local Administrator Credential Dumping

A local Administrator account can be used to remotely
extract local SAM hashes and cached domain credentials.

Example:

    secretsdump.py <HOST>/<USER>:<PASSWORD>@<TARGET_IP> -output local_dump

The tool can retrieve:

- Local SAM hashes
- Cached domain credentials
- LSA-related credential material

## MSCacheV2 / DCC2

Domain Cached Credentials are stored locally so that users
can authenticate when the machine cannot contact the domain.

These hashes are commonly represented as:

    $DCC2$

Unlike NTLM hashes, DCC2 hashes cannot be directly used for
Pass-the-Hash authentication.

They can instead be cracked offline.

## Cracking DCC2

John the Ripper can be used with the `mscash2` format:

    john --format=mscash2 dc2_hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

Hashcat can also be used for offline cracking.

## Domain Controller Credential Dumping

Once Domain Administrator privileges are obtained,
secretsdump can target the Domain Controller.

Example:

    secretsdump.py <DOMAIN>/<USER>:<PASSWORD>@<DC_IP> -just-dc -output dc_dump

The `-just-dc` option performs the DRSUAPI-based extraction
of domain credential material.

## DRSUAPI / DCSync

The technique abuses the Directory Replication Service
protocol to retrieve credential information from the
Domain Controller.

The resulting information can include:

- Domain user NTLM hashes
- Kerberos keys
- Computer account hashes
- krbtgt material

## Credential Escalation Chain

The room demonstrated the following progression:

    Local Administrator
          ↓
    secretsdump
          ↓
    Local SAM / Cached Credentials
          ↓
    Recover Domain User Password
          ↓
    Domain User Access
          ↓
    Domain Administrator
          ↓
    secretsdump -just-dc
          ↓
    Domain Credential Dump
          ↓
    NTLM Hash
          ↓
    Pass-the-Hash
          ↓
    SYSTEM on Domain Controller

## Pass-the-Hash

Once a Domain Administrator NTLM hash is available, the
plaintext password is not necessarily required.

The hash can be used for Pass-the-Hash authentication.

Example with PsExec:

    psexec.py '<DOMAIN>/<USER>@<DC_IP>' -hashes :<NTLM_HASH>

A successful execution can provide a SYSTEM shell on the
Domain Controller.

## Key Takeaways

secretsdump demonstrates how credential harvesting can be
performed remotely without directly copying sensitive
credential databases from the target.

The technique can progress from local account hashes and
cached credentials to full domain credential extraction
when sufficient privileges are obtained.