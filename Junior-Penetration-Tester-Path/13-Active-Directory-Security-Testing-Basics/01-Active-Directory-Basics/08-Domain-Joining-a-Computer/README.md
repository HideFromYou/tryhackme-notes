# 08 - Domain Joining a Computer

## Overview

Joined a Windows server to an existing Active Directory domain.

## Topics Covered

- Domain joining
- DNS configuration
- Domain credentials
- PowerShell
- Add-Computer
- Reboot after domain joining
- Domain authentication

## Domain Joining Process

Three main steps were performed.

### 1. DNS

The server needs to be able to locate and communicate with
the Domain Controller.

Therefore, the server's DNS configuration was pointed to
the Domain Controller.

### 2. Credentials

Joining a computer to a domain requires credentials from an
AD account that has permission to perform the operation.

The account does not necessarily have to be Domain
Administrator, but it needs the appropriate permissions.

### 3. Domain Joining

PowerShell's `Add-Computer` command was used to join the
server to the domain.

Example:

    Add-Computer -DomainName <domain> -Credential <credentials>

## Reboot

After the computer has been successfully joined:

    Restart-Computer -Force

The reboot completes the domain-joining process.

## Domain Authentication

After joining the domain, the machine can authenticate users
using domain credentials instead of only local accounts.

## Key Takeaways

The basic domain-join workflow is:

    DNS
      ↓
    Valid AD credentials
      ↓
    Add-Computer
      ↓
    Reboot
      ↓
    Domain authentication