# 04 - Kerberos Authentication

## Overview

Explored Kerberos authentication and the main components
involved in authenticating to services in an Active Directory
environment.

## Topics Covered

- Kerberos
- Key Distribution Center (KDC)
- Ticket Granting Ticket (TGT)
- Ticket Granting Service (TGS)
- Service Principal Names (SPNs)
- Session Keys
- Kerberos tickets
- Credential Cache
- KRB5CCNAME
- Kerberos authentication with SMB

## Kerberos

Kerberos is a ticket-based authentication protocol and the
default authentication protocol used by modern Windows domains.

## KDC

The Key Distribution Center is responsible for issuing
Kerberos tickets.

It contains:

- Authentication Service (AS)
- Ticket Granting Service (TGS)

## TGT

The Ticket Granting Ticket is issued after initial
authentication.

The TGT allows the user to request service tickets without
re-authenticating with the password each time.

## TGS

A Ticket Granting Service ticket is issued for a specific
service.

The ticket can then be presented to the requested service.

## SPN

A Service Principal Name identifies a service instance
associated with an account.

SPNs are important when requesting Kerberos service tickets.

## Authentication Flow

    User
      |
      | Authentication
      v
    KDC
      |
      | TGT
      v
    User
      |
      | Request TGS
      v
    KDC
      |
      | TGS
      v
    User
      |
      | Present TGS
      v
    Service

## Kerberos Credential Cache

Kerberos tickets can be stored in a credential cache.

The environment variable used to specify the cache is:

    KRB5CCNAME

## SMB and Kerberos

When using Kerberos authentication with SMB, the hostname
should be used rather than the IP address.

Example:

    smbclient.py <domain>/<user>@<hostname> -k -no-pass

## Key Takeaways

- Kerberos is ticket-based.
- The KDC issues Kerberos tickets.
- TGTs are used to request service tickets.
- TGS tickets authenticate users to specific services.
- SPNs identify services.
- Kerberos relies on correct hostnames/DNS.