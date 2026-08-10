# 06 - Proxy Challenge Room

## Overview

A practical challenge focused on applying Active Directory
and lateral movement knowledge through a proxy.

The challenge required routing traffic through an
intermediate system to reach internal resources.

## Objective

Use the available access and network path to move through
the environment and ultimately obtain Administrator-level
access.

## Main Concepts

- Active Directory
- Lateral Movement
- Proxying
- Pivoting
- Network Segmentation
- Credential Reuse
- Restricted Network Access

## Challenge Concept

The challenge reinforces the idea that internal services
may not be directly reachable from the attacker's machine.

The attacker must use an intermediate host as a proxy
to reach the target network.

## Methodology

    Initial Access
          ↓
    Identify Network Restrictions
          ↓
    Identify Pivot Host
          ↓
    Route Traffic Through Proxy
          ↓
    Access Internal Resources
          ↓
    Perform Lateral Movement
          ↓
    Reach Administrator Access

## Key Takeaway

A restricted network does not necessarily prevent access
if a compromised host exists that can communicate with the
target network.

Pivoting turns that compromised host into a bridge between
otherwise isolated network segments.
```

### 07 — `07-Forward-Challenge-Room/README.md`

````markdown
# 07 - Forward Challenge Room

## Overview

A practical Active Directory lateral movement challenge
starting from an assumed initial compromise.

The objective was to move forward through the domain,
escalate privileges and reach Administrator-level access.

## Starting Point

The challenge provides an initial compromised domain
account.

The starting credentials should be kept out of public
repositories when documenting the lab.

## Objectives

- Enumerate the compromised environment
- Identify lateral movement opportunities
- Reuse available credentials
- Move between hosts
- Escalate privileges
- Reach the final Administrator objective

## Methodology

    Initial Domain Access
          ↓
    Enumeration
          ↓
    Identify Credentials
          ↓
    Lateral Movement
          ↓
    Privilege Escalation
          ↓
    Administrator Access

## Techniques

The challenge reinforces concepts from the room including:

- Remote execution
- Credential reuse
- Pass-the-Hash
- Kerberos abuse
- Lateral movement
- Active Directory enumeration

## Key Takeaway

Once an attacker has valid access to an Active Directory
environment, the objective becomes identifying how that
access can be extended to additional systems and higher
privileges.
```

### 08 — `08-Conclusion/README.md`

````markdown
# 08 - Conclusion

## Overview

This room covered the fundamentals of Active Directory
lateral movement, starting from a compromised WebServer
and progressing towards the Domain Controller.

Three core techniques were demonstrated:

- Remote Execution
- Pass-the-Hash
- Pivoting

## Remote Execution

PsExec was used to obtain a SYSTEM shell on a workstation
through SMB.

Evil-WinRM was then used to obtain a PowerShell session
through WinRM.

## Pass-the-Hash

A harvested local Administrator NT hash was reused to
authenticate to another host without knowing the plaintext
password.

NetExec was used to identify where the same local
Administrator hash was valid.

Impacket was then used to obtain remote SYSTEM access.

## Pivoting

An SSH SOCKS proxy was created through the compromised
WebServer.

This allowed traffic from the AttackBox to reach the
restricted internal network containing the Domain Controller.

The same pivot was then used to reach the final target.

## Overall Attack Chain

    Compromised WebServer
          ↓
    Remote Execution
          ↓
    Compromised Workstation
          ↓
    Harvest NTLM Hash
          ↓
    Pass-the-Hash
          ↓
    Compromise SERVER1
          ↓
    Discover Domain Admin Hash
          ↓
    SSH SOCKS Pivot
          ↓
    Reach Restricted Network
          ↓
    Domain Controller
          ↓
    Administrator / SYSTEM Access

## Mitigations

The room covered defensive controls including:

- Windows LAPS
- SMB Signing
- NTLM Restrictions
- Host Firewall Rules
- Network Segmentation
- Privileged Access Workstations

## Main Tools

    Impacket
    NetExec
    Evil-WinRM
    SSH
    ProxyChains
    Mimikatz
    Rubeus
    Chisel
    Ligolo-ng

## Key Takeaways

Lateral movement is an iterative process.

The core loop is:

    Move
      ↓
    Harvest
      ↓
    Move Again
      ↓
    Harvest Again

Each compromised host can provide new credentials,
permissions or network access that enables the next step.

## What's Next

The room introduces deeper topics that can be explored
in later Active Directory modules:

- PsExec
- SMBExec
- WMI
- DCOM
- AtExec
- Pass-the-Ticket
- Overpass-the-Hash
- S4U abuse
- Chisel
- Ligolo-ng
- Double Pivoting
- ProxyChains
- Advanced lateral movement challenges
```

Το υλικό επιβεβαιώνει ότι το room καλύπτει τα τρία βασικά pillars **Remote Execution → Credential Reuse → Pivoting**, με PsExec/Evil-WinRM, Pass-the-Hash και SSH SOCKS pivoting. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}