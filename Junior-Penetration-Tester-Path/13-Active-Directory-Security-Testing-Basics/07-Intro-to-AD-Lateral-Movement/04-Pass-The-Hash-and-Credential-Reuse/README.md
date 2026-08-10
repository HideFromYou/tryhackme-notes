# 04 - Pass-The-Hash and Credential Reuse

## Overview

This task focused on reusing NTLM hashes to authenticate
to remote systems without knowing the plaintext password.

## Topics Covered

- NTLM
- NT Hash
- Net-NTLMv2
- Pass-the-Hash
- Local Administrator hashes
- Credential Reuse
- NetExec
- Impacket
- LAPS
- PsExec

## Pass-the-Hash

NTLM authentication uses a challenge-response mechanism.

The important concept is that the NT hash can be used
during authentication without knowing the plaintext
password.

Therefore:

    NT Hash
       ↓
    Authentication
       ↓
    Remote Access

## NT Hash vs Net-NTLMv2

These two values should not be confused.

### NT Hash

Typically obtained from:

- SAM
- NTDS.dit
- LSASS
- Mimikatz
- secretsdump

Format:

    32 hexadecimal characters

An NT hash can be used for Pass-the-Hash.

### Net-NTLMv2

Typically captured from network authentication using
techniques such as:

- Responder
- NTLM coercion
- LLMNR poisoning

Net-NTLMv2 is a challenge-response artefact and cannot
directly be used for Pass-the-Hash.

It normally needs to be:

- Cracked offline
- Relayed

## Credential Reuse

A harvested local Administrator NT hash can be tested
against multiple hosts.

NetExec can authenticate using the hash:

    nxc smb <TARGET_IPS> -u Administrator -H <NT_HASH> --local-auth

The `--local-auth` option is important when testing
local accounts.

## Why LAPS Matters

If the same local Administrator password is reused across
multiple systems, the same NT hash may work on multiple
machines.

This creates a major lateral movement risk.

Windows LAPS addresses this by providing unique,
automatically managed local Administrator passwords.

## Pass-the-Hash with Impacket

Once a valid NT hash has been identified, Impacket tools
can authenticate using the hash.

Example:

    psexec.py '<DOMAIN>/<USER>@<TARGET_IP>' -hashes :<NT_HASH>

The plaintext password is not required.

## Attack Flow

    Compromised Host
          ↓
    Harvest NT Hash
          ↓
    Test Hash Against Hosts
          ↓
    Identify Reused Credentials
          ↓
    Pass-the-Hash
          ↓
    Remote SYSTEM Access
          ↓
    Harvest More Credentials

## Key Takeaways

Pass-the-Hash demonstrates why protecting NT hashes is
critical.

A plaintext password is not always required for lateral
movement.

A reusable local Administrator hash can provide access
to multiple hosts when local credentials are not properly
managed.