# 03 - OSINT and Target Reconnaissance

## Overview

Explored how OSINT and reconnaissance can be used to build
potential username lists and validate them against an
Active Directory domain.

## Topics Covered

- OSINT
- Employee enumeration
- Username formats
- LinkedIn
- GitHub / GitLab
- Corporate websites
- Job listings
- Public data breaches
- Kerbrute
- Kerberos username enumeration
- DNS enumeration
- SRV records

## OSINT Sources

Potential usernames can be collected from:

- LinkedIn
- GitHub
- GitLab
- Public data breaches
- Corporate websites
- Job listings

## Common Username Formats

Common AD username formats include:

    first.last
    firstlast
    flast
    first.l
    first
    last.first

Example:

    jane.smith
    janesmith
    jsmith

The objective is to identify the naming convention used by
the target organisation.

## Username Enumeration with Kerbrute

Kerbrute can validate potential usernames by interacting
with Kerberos.

Example:

    kerbrute userenum -d thm.loc --dc <DC_IP> /root/usernames.txt

Save the results:

    kerbrute userenum -d thm.loc --dc <DC_IP> /root/usernames.txt -o valid_users.txt

## How It Works

For a non-existent username, the KDC returns:

    KDC_ERR_C_PRINCIPAL_UNKNOWN

For an existing username, the KDC requests pre-authentication.

This behaviour allows username validation.

## Important Detection Point

Kerberos username enumeration does not trigger normal account
lockouts, but it can generate Windows Event ID:

    4768

## DNS Enumeration

Identify Domain Controllers:

    nslookup -type=SRV _ldap._tcp.dc._msdcs.thm.loc

Identify the Kerberos KDC:

    nslookup -type=SRV _kerberos._tcp.thm.loc

Identify mail servers:

    nslookup -type=MX thm.loc <DC_IP>

## Key Takeaways

The goal of reconnaissance is to transform public information
into a validated list of potential AD usernames.

That list can then be used in later credential attacks such
as password spraying.