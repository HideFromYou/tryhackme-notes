# 06 - Mitigations

## Overview

This task shifted from the offensive techniques used in the
room to the defensive controls that can prevent or limit
credential harvesting and lateral movement.

## Topics Covered

- Windows LAPS
- Least Privilege
- Local Administrator Restrictions
- SMB Signing
- NTLM Restrictions
- Credential Guard
- Host Firewall Rules
- Network Segmentation
- Privileged Access Workstations
- Monitoring and Detection
- Windows Event IDs
- Sysmon

## Windows LAPS

Windows LAPS automatically generates unique local
Administrator passwords for domain-joined machines.

This prevents the same local Administrator password and
therefore the same NTLM hash from being reused across
multiple systems.

Windows LAPS also supports:

- Automatic password rotation
- Password history
- Password encryption in Active Directory
- Entra ID storage
- DSRM password management

## Restricting Local Administrator Rights

Users should not have unnecessary local Administrator
privileges on other systems.

Administrative access should follow the principle of
least privilege.

A tiered administration model should separate:

    Tier 0
    Domain Controllers / Domain Admins

    Tier 1
    Servers / Server Administrators

    Tier 2
    Workstations / Workstation Administrators

## SMB Signing

SMB signing helps protect the integrity and origin of SMB
communications.

The following Group Policy settings should be enforced:

    Microsoft network server:
    Digitally sign communications (always)

    Microsoft network client:
    Digitally sign communications (always)

SMB signing reduces the effectiveness of several SMB-based
attacks.

## Restricting NTLM

Pass-the-Hash depends heavily on NTLM authentication.

NTLM can be audited and progressively restricted through
Group Policy.

Relevant settings include:

    Restrict NTLM:
    NTLM authentication in this domain

    Restrict NTLM:
    Audit NTLM authentication in this domain

A practical approach is:

    Audit
      ↓
    Identify Dependencies
      ↓
    Remediate
      ↓
    Restrict NTLM

## Credential Guard

Credential Guard uses virtualization-based security to
isolate sensitive LSASS credential material.

This makes it significantly harder for tools such as
Mimikatz to extract NTLM hashes and Kerberos credentials
from LSASS memory.

## Host Firewall Rules

Workstations should generally not need direct administrative
connections to other workstations.

Firewall rules can restrict:

    SMB   TCP 445
    WinRM TCP 5985
    RDP   TCP 3389

while still allowing legitimate management servers and
jump hosts.

## Network Segmentation

Network segmentation limits which systems can communicate
with each other.

Recommended separation includes:

    Workstations
        ↓
    Servers
        ↓
    Domain Controllers

Domain Controllers should reside in dedicated, hardened
network segments with restricted inbound access.

## Privileged Access Workstations

Privileged Access Workstations (PAWs) are dedicated,
hardened systems used for Tier 0 administrative tasks.

The goal is to prevent privileged credentials from ever
being exposed on ordinary workstations.

This reduces the opportunity to harvest:

- Domain Administrator hashes
- Kerberos tickets
- Authentication tokens

## Monitoring and Detection

Important Windows Event IDs covered include:

| Event ID | Log | Detection |
|---:|---|---|
| 4624 Type 3 | Security | Unexpected network logon |
| 4624 Type 10 | Security | Unexpected remote interactive logon |
| 4648 | Security | Explicit credential use |
| 7045 | System | New service installation |
| 4698 | Security | Scheduled task creation |
| 4688 | Security | Process creation |

## Sysmon

Sysmon provides additional process-level telemetry.

Important events include:

    Event ID 1
    Process creation

    Event ID 10
    Process access

Event ID 10 can be particularly useful for detecting
unexpected processes accessing LSASS.

## Detection Strategy

Credential theft and lateral movement can generate unusual
authentication patterns.

Examples include:

- One account authenticating to many hosts quickly
- Workstations connecting to other workstations over SMB
- Service accounts logging on interactively
- Unexpected remote administrative activity
- New services with unusual names
- Unexpected processes accessing LSASS

## Key Takeaways

Credential harvesting can be significantly harder when
organisations combine:

    Least Privilege
          ↓
    Windows LAPS
          ↓
    Credential Guard
          ↓
    NTLM Restrictions
          ↓
    SMB Signing
          ↓
    Network Segmentation
          ↓
    PAWs
          ↓
    Monitoring & Detection

No single control eliminates credential theft completely.
Layered security controls reduce both the likelihood of
credential harvesting and the attacker's ability to reuse
the recovered credentials.