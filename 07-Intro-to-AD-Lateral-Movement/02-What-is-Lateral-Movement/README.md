# 02 - What is Lateral Movement?

## Overview

Lateral movement is the process of moving from one
compromised host to another using valid credentials,
hashes or authentication tickets.

Unlike initial access, lateral movement relies primarily
on legitimate authentication mechanisms.

## Why Lateral Movement Matters

A compromised workstation may provide an initial foothold,
but valuable resources are usually located on other systems.

Examples include:

- Domain Controllers
- Servers
- Service accounts
- Backup servers
- Administrative workstations

The attacker can use credentials harvested from one host
to authenticate to another.

This creates the cycle:

    Move
      ↓
    Harvest
      ↓
    Move Again
      ↓
    Harvest Again

## Three Pillars of Lateral Movement

### Remote Execution

Executing commands on a remote Windows system through
legitimate administration protocols.

Examples:

- PsExec
- WinRM
- WMI
- DCOM
- SMBExec
- AtExec

### Credential Reuse

Using recovered authentication material to authenticate
to another host.

Examples:

- Pass-the-Hash
- Pass-the-Ticket
- Overpass-the-Hash

### Pivoting

Using a compromised host as a relay to reach systems on
a network segment that is not directly accessible.

Examples:

- SSH Local Port Forwarding
- SSH Dynamic Port Forwarding
- SOCKS Proxy
- ProxyChains

## Requirements

Two main requirements are needed for most lateral movement
techniques.

### Valid Credentials

Authentication material can include:

- Plaintext password
- NTLM hash
- Kerberos ticket

### Administrative Access

Most remote execution techniques require local
Administrator privileges on the target.

WinRM can also allow access to members of:

    Remote Management Users

## Local Administrator vs Domain Administrator

Local Administrator access does not automatically mean
Domain Administrator access.

However, a workstation with local Administrator access
may contain cached credentials or active sessions belonging
to privileged domain users.

## Main Tools

| Tool | Purpose |
|---|---|
| Impacket | Remote execution |
| NetExec | Authentication and execution |
| Evil-WinRM | WinRM sessions |
| SSH | Tunnelling and pivoting |
| Mimikatz | Credential and ticket operations |
| Rubeus | Kerberos operations |
| Chisel | Network tunnelling |
| Ligolo-ng | Advanced tunnelling |

## Key Takeaway

Lateral movement is an iterative process.

Each newly compromised host may provide credentials or
access that enables the next movement through the network.