# 01 - Introduction

## Overview

Introduction to unauthenticated Active Directory enumeration.

The goal of the room is to understand how much information
can be gathered from an Active Directory environment before
obtaining valid credentials.

## Topics Covered

- Network reconnaissance
- Host discovery
- Service enumeration
- SMB
- LDAP
- RPC
- Kerberos
- Username enumeration
- Password spraying

## Enumeration Methodology

The general workflow is:

    Network Discovery
          ↓
    Service Enumeration
          ↓
    SMB Enumeration
          ↓
    Domain Enumeration
          ↓
    Username Enumeration
          ↓
    Password Policy
          ↓
    Password Spraying
          ↓
    Initial Credentials

## Key Takeaway

Unauthenticated enumeration can reveal enough information
to identify hosts, services, users and potential attack paths
inside an Active Directory environment.