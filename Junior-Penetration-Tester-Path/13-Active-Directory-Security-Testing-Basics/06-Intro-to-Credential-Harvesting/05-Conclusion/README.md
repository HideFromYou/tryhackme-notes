# 05 - Conclusion

## Overview

This task summarised the credential harvesting techniques
covered throughout the room.

The room demonstrated how credentials can be recovered from
different Windows and Active Directory storage locations and
then reused to move deeper into the environment.

## Credential Stores Covered

- LSASS Memory
- SAM
- SYSTEM
- LSA Secrets
- DPAPI Vault
- NTDS.dit
- Cached Domain Credentials

## Main Tools

    Mimikatz
    secretsdump.py
    John the Ripper
    Hashcat
    PsExec

## Overall Attack Chain

The room demonstrated a progression from local Administrator
access to Domain Administrator access:

    Local Administrator
          ↓
    Credential Harvesting
          ↓
    Local Hashes / Cached Credentials
          ↓
    Credential Cracking
          ↓
    Domain User Access
          ↓
    Domain Administrator
          ↓
    NTDS.dit / DCSync
          ↓
    Domain Credential Material
          ↓
    Pass-the-Hash
          ↓
    Domain Controller SYSTEM Access

## Main Lessons

Credentials are stored throughout Windows and Active
Directory for different purposes.

A compromised workstation can therefore contain valuable
credential material even when the target user's plaintext
password is not directly available.

The most important concepts covered were:

- Identifying credential stores
- Understanding the type of credential material stored
- Choosing the appropriate extraction technique
- Cracking hashes offline when required
- Reusing recovered credentials
- Moving laterally through the environment
- Extracting domain-wide credentials with sufficient
  privileges

## Final Takeaway

Credential harvesting is a key post-exploitation skill.

The important concept is not simply knowing how to run a
credential-dumping tool, but understanding where credentials
are stored and how the recovered material can be used to
progress through an Active Directory environment.