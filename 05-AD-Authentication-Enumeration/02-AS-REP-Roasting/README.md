# 02 - AS-REP Roasting

## Overview

AS-REP Roasting is a Kerberos attack against user accounts
that have Kerberos pre-authentication disabled.

The vulnerable accounts have the:

    UF_DONT_REQUIRE_PREAUTH

flag enabled.

## Topics Covered

- Kerberos pre-authentication
- AS-REP
- UF_DONT_REQUIRE_PREAUTH
- Rubeus
- GetNPUsers.py
- Impacket
- AS-REP hash extraction
- Hashcat
- Offline password cracking

## Why Is It Vulnerable?

During normal Kerberos authentication, pre-authentication
requires the user to prove their identity before the KDC
returns the AS-REP.

When pre-authentication is disabled, the KDC can return an
encrypted AS-REP without first verifying the user's identity.

The resulting encrypted data can be captured and cracked
offline.

## Two Phases

AS-REP Roasting consists of:

    Enumeration
        ↓
    Exploitation

### Phase 1 - Enumeration

The objective is to identify accounts with Kerberos
pre-authentication disabled.

### Rubeus

On Windows:

    Rubeus.exe asreproast

Rubeus can automatically identify vulnerable accounts and
retrieve their AS-REP hashes.

### GetNPUsers.py

From Linux or the AttackBox:

    GetNPUsers.py <DOMAIN>/ -dc-ip <DC_IP> \
    -usersfile users.txt \
    -format hashcat \
    -outputfile hashes.txt \
    -no-pass

The command checks the supplied usernames and retrieves
AS-REP hashes from vulnerable accounts.

## Phase 2 - Exploitation

Once hashes have been obtained, they can be cracked offline.

### Hashcat

AS-REP hashes use Hashcat mode:

    18200

Example:

    hashcat -m 18200 hashes.txt wordlist.txt

The supplied wordlist can be:

    /usr/share/wordlists/rockyou.txt

## Attack Flow

    User Enumeration
          ↓
    Identify Accounts Without Pre-authentication
          ↓
    Request AS-REP
          ↓
    Retrieve Encrypted Hash
          ↓
    Offline Cracking
          ↓
    Recover Password
          ↓
    Authenticate as Compromised User

## Mitigations

- Enforce Kerberos pre-authentication
- Use strong, complex passwords
- Monitor anomalous AS-REP requests on the KDC

## Key Takeaways

AS-REP Roasting is a low-noise Kerberos attack that can be
performed without knowing the user's password.

The key requirement is that the target account has
UF_DONT_REQUIRE_PREAUTH enabled.