# 05 - Weaknesses in AD Authentication

## Overview

Explored weaknesses in NTLM and Kerberos authentication and
performed practical demonstrations of common authentication
attacks.

## NTLM Weaknesses

- Weak cryptography
- Pass-the-Hash
- NTLM Relay
- Downgrade attacks
- Lack of mutual authentication

## Kerberos Weaknesses

- Kerberoasting
- AS-REP Roasting
- Pass-the-Ticket
- Overpass-the-Hash
- Golden Ticket
- Silver Ticket

## Configuration Weaknesses

- Weak passwords
- Password spraying
- Misconfigured delegation
- Stale credentials

## Weak Password Hashing

NTLM hashes are unsalted and use the MD4 hashing algorithm.

Weak passwords can therefore be vulnerable to offline
cracking attacks.

Hashcat can be used to crack NTLM hashes.

Example:

    hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt

Display recovered passwords:

    hashcat -m 1000 hash.txt --show

## Pass-the-Hash

Pass-the-Hash allows an attacker to authenticate using an
NTLM hash without knowing the plaintext password.

Example:

    smbclient.py <domain>/<user>@<target> -hashes <LM_hash>:<NTLM_hash>

## Kerberoasting

Kerberoasting targets service accounts with registered SPNs.

An authenticated domain user can request service tickets.
The resulting ticket can be extracted and cracked offline.

Example:

    GetUserSPNs.py <domain>/<user>:<password> -dc-ip <DC_IP> -request

TGS-REP hashes can be cracked using Hashcat:

    hashcat -m 13100 service_ticket.txt /usr/share/wordlists/rockyou.txt

## Golden Ticket

Golden Ticket attacks target the KRBTGT account.

If the KRBTGT password hash is compromised, an attacker can
forge Kerberos TGTs and impersonate users in the domain.

This can lead to complete domain compromise.

## AS-REP Roasting

Targets accounts where Kerberos pre-authentication is disabled.

## Pass-the-Ticket

Reuses valid Kerberos tickets to authenticate as their owner.

## Overpass-the-Hash

Uses an NTLM hash to request a Kerberos TGT.

## Silver Ticket

Forges Kerberos service tickets using a service account's
password hash.

## Key Takeaways

Weak credentials, protocol weaknesses and compromised
authentication material can allow attackers to gain
unauthorised access and potentially compromise the domain.