# 02 - Authentication in AD

## Overview

Explored how authentication works inside an Active Directory
environment and the difference between authentication and
authorisation.

## Topics Covered

- Authentication
- Authentication material
- Username and password
- Certificates
- Password hashes
- Authentication vs Authorisation
- NetNTLM
- Kerberos
- LDAP
- SMB

## Authentication Material

Authentication can use different forms of credentials:

- Username and password
- Certificates
- Password hashes

The purpose is always the same:

    Prove your identity

## Authentication vs Authorisation

Authentication:

    "Who are you?"

Authorisation:

    "What are you allowed to access?"

Example:

    Authentication
        ↓
    User identity verified
        ↓
    Authorisation
        ↓
    Permissions are evaluated

## AD Authentication Protocols

### NetNTLM

A challenge-response authentication protocol originating
from Windows NT.

### Kerberos

A ticket-based authentication protocol that became the
default authentication mechanism in Windows 2000 and remains
the preferred protocol today.

## Service Protocols

Protocols such as:

- LDAP
- SMB
- WebDAV

may be encountered in AD environments, but they rely on
NTLM or Kerberos for authentication.

## Key Takeaways

Authentication establishes identity.

Authorisation determines what the authenticated identity
is allowed to do.