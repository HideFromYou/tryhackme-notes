# 01 - Introduction

## Overview

Introduction to Active Directory Breaching and the process of
obtaining the first valid domain credentials.

## Topics Covered

- What AD breaching means
- Initial access in an AD environment
- Importance of initial credentials
- AD attack surface
- SMB
- LDAP
- HTTP/HTTPS
- Kerberos
- DNS
- Unauthenticated vs authenticated starting positions
- Breaching methodology

## AD Breaching

AD breaching is the process of obtaining an initial set of
valid Active Directory credentials when starting without
credentials.

Obtaining the first valid account allows an attacker to:

- Enumerate the domain
- Discover users and groups
- Identify computers
- Discover Group Policies
- Identify trust relationships
- Search for privilege escalation paths
- Move laterally

## AD Attack Surface

Important services include:

| Service | Port | Purpose |
|---|---:|---|
| SMB | 445 | File shares, printers, remote administration |
| LDAP | 389/636 | Active Directory directory services |
| HTTP/HTTPS | 80/443 | Internal web applications and services |
| Kerberos | 88 | Domain authentication |
| DNS | 53 | Name resolution and AD infrastructure discovery |

## Starting Positions

### Unauthenticated / Black-box

Network access is available but no valid AD credentials are
known.

The attacker must:

- Enumerate
- Discover credentials
- Perform password spraying
- Use coercion techniques

### Authenticated / Grey-box

The attacker already has valid low-privileged credentials.

The attacker can immediately begin:

- AD enumeration
- User enumeration
- Group enumeration
- Computer enumeration
- Attack-path discovery

## Key Takeaways

The first objective in an AD attack chain is obtaining valid
credentials.

From there, authentication provides access to information
that can reveal further attack paths.