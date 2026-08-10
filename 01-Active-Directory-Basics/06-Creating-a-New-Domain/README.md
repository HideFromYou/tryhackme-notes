# 06 - Creating a New Domain

## Overview

Created a new child domain and promoted a server to a
Domain Controller.

## Scenario

The existing parent domain was:

    thm.loc

A new banking domain was created as:

    tbm.thm.loc

This creates a child domain under the parent domain.

## Topics Covered

- Child Domains
- Domain Controller promotion
- DNS configuration
- Parent Domain credentials
- Active Directory Domain Services
- PowerShell automation
- Domain promotion
- Reboot after promotion

## Domain Promotion Process

The provided PowerShell script performed several steps.

### 1. DNS Configuration

The new server was configured to use the existing
Domain Controller as its DNS server.

### 2. Administrator Password

The Administrator account password was configured before
promotion.

### 3. Parent Domain Credentials

Credentials from the parent domain were required to create
the child domain.

### 4. AD Services

Active Directory Domain Services and administration tools
were required for the promotion.

### 5. Domain Promotion

PowerShell's ADDSDeployment functionality was used to promote
the server to a Domain Controller.

The resulting child domain was:

    tbm.thm.loc

## Important PowerShell Commands

Execute the provided domain installation script:

    C:\install-domain.ps1

After the promotion:

    Restart-Computer -Force

## After Promotion

After rebooting, the new Domain Controller becomes part of the
new child domain.

The environment can then be managed using Active Directory
tools.

## Key Takeaways

Creating a child domain requires:

- Correct DNS configuration
- Parent-domain administrative credentials
- AD DS installation/configuration
- Domain promotion
- Reboot and post-promotion configuration