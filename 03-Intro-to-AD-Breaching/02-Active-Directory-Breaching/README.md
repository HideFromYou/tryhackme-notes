# 02 - Active Directory Breaching

## Overview

Explored what AD breaching means and the common attack surface
available when attempting to obtain the first valid domain
credentials.

## Topics Covered

- Initial credentials
- AD attack surface
- SMB
- LDAP
- HTTP/HTTPS
- Kerberos
- DNS
- Black-box attacks
- Grey-box attacks

## Why Initial Credentials Matter

Even a low-privileged domain account can provide access to
information that is normally unavailable to unauthenticated
users.

Once authenticated, an attacker can query information about:

- Users
- Groups
- Computers
- Group Policies
- Trust relationships

This information can reveal misconfigurations and additional
attack paths.

## Common Attack Surface

### SMB

    TCP 445

Used for:

- File shares
- Printers
- Remote administration
- Credential testing

### LDAP

    TCP 389
    TCP 636

Used to query and manage Active Directory objects.

Misconfigured devices may expose stored LDAP credentials.

### HTTP / HTTPS

Internal web services may expose:

- Credentials
- Configuration files
- Build logs
- Source code
- Administrative interfaces

### Kerberos

    TCP/UDP 88

The primary AD authentication protocol.

Kerberos behaviour can also be used for username enumeration.

### DNS

    TCP/UDP 53

Used to identify:

- Domain Controllers
- Kerberos infrastructure
- Mail servers
- Other AD services

## Key Takeaways

AD breaching is not necessarily a single attack.

The initial foothold can come from multiple services and
misconfigurations across the environment.