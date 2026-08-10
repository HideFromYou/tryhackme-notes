# 07 - Intro to AD Lateral Movement

## Overview

This folder contains my notes and hands-on work from the
TryHackMe Introduction to AD Lateral Movement room.

The room focuses on moving from an already compromised host
to other systems inside an Active Directory environment by
using valid credentials, NTLM hashes and network pivoting.

The practical scenario starts from a compromised WebServer
and demonstrates how lateral movement can eventually lead to
the Domain Controller.

## Topics Covered

- Active Directory Lateral Movement
- Remote Execution
- Credential Reuse
- Pass-the-Hash
- NTLM Hashes
- Kerberos Tickets
- Pivoting
- SSH Tunnelling
- SOCKS Proxy
- ProxyChains
- PsExec
- Evil-WinRM
- WMI
- DCOM
- SMBExec
- AtExec
- NetExec
- Impacket
- Network Segmentation
- Windows LAPS
- SMB Signing
- NTLM Restrictions
- Host Firewall Rules
- Privileged Access Workstations

## What Is Lateral Movement?

Lateral movement is the process of moving from one
compromised host to another using valid authentication
material.

The authentication material can include:

- Plaintext passwords
- NTLM hashes
- Kerberos tickets

The basic idea is:

    Compromise Host
          ↓
    Harvest Credentials
          ↓
    Authenticate to Another Host
          ↓
    Harvest More Credentials
          ↓
    Move Again

This creates an iterative:

    Move → Harvest → Move Again

cycle.

## Three Pillars of Lateral Movement

### 1. Remote Execution

Remote execution allows commands to be executed on another
Windows system through legitimate administration protocols.

Techniques covered include:

- PsExec
- WinRM
- WMI
- DCOM
- SMBExec
- AtExec

### 2. Credential Reuse

Recovered authentication material can be reused to access
additional systems.

The main technique covered was:

    Pass-the-Hash

The room also introduced:

- Pass-the-Ticket
- Overpass-the-Hash

### 3. Pivoting

Pivoting uses a compromised host as a relay to access
network segments that cannot be reached directly.

Techniques covered include:

- SSH tunnelling
- SSH local port forwarding
- SSH dynamic port forwarding
- SOCKS proxies
- ProxyChains

## Requirements for Lateral Movement

Two important requirements were identified.

### Valid Authentication Material

This can be:

- Plaintext password
- NTLM hash
- Kerberos ticket

### Administrative Access

Most remote execution methods require local Administrator
access on the target.

WinRM can also allow access through the:

    Remote Management Users

group.

## Remote Execution

The room demonstrated remote execution using PsExec and
Evil-WinRM.

### PsExec

PsExec uses SMB to upload and execute a service on the
target.

The general process is:

    SMB Authentication
          ↓
    ADMIN$ Access
          ↓
    Upload Service Binary
          ↓
    Service Creation
          ↓
    Service Execution
          ↓
    SYSTEM Shell

### Evil-WinRM

Evil-WinRM provides an interactive PowerShell session
through WinRM.

Example:

    evil-winrm -i <TARGET_IP> -u <USERNAME> -p '<PASSWORD>'

WinRM operates over HTTP/HTTPS and provides an alternative
to service-based execution.

## Pass-the-Hash

Pass-the-Hash allows authentication using an NTLM hash
without knowing the plaintext password.

The basic flow is:

    NTLM Hash
        ↓
    Authentication
        ↓
    Remote Access

NetExec can be used to test whether a local Administrator
hash is valid on other systems.

Example:

    nxc smb <TARGET_IP> -u Administrator -H <NT_HASH> --local-auth

Impacket can then use the hash for remote execution:

    psexec.py '<DOMAIN>/<USER>@<TARGET_IP>' -hashes :<NT_HASH>

## LAPS

The room demonstrated the security risk of reusing the same
local Administrator password across multiple systems.

If the same password is reused, the same NTLM hash can also
work on multiple machines.

Windows LAPS helps prevent this by providing unique,
automatically managed local Administrator passwords.

## Pivoting

The network was segmented so that the Domain Controller was
not directly reachable from the initial attack position.

The compromised WebServer could communicate with the
restricted internal network.

Therefore:

    AttackBox
        ↓
    WebServer
        ↓
    Internal Network
        ↓
    Domain Controller

## SSH SOCKS Proxy

Dynamic SSH forwarding can create a SOCKS proxy:

    ssh -f -D 1080 <USER>@<PIVOT_IP> -N

The local SOCKS proxy listens on:

    127.0.0.1:1080

Traffic can then be routed through the compromised host.

## ProxyChains

ProxyChains can route supported TCP traffic through the
SOCKS proxy.

Example configuration:

    socks4 127.0.0.1 1080

Commands can then be executed through the proxy:

    proxychains <COMMAND>

## Overall Attack Chain

The practical progression covered in the room was:

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
    SYSTEM / Administrator Access

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

## Mitigations

The room also covered defensive controls that can break
different stages of lateral movement.

### Windows LAPS

Provides unique local Administrator passwords and prevents
the same local credentials from being reused across hosts.

### SMB Signing

Helps protect SMB communications and reduces the effectiveness
of certain SMB-based attacks.

### NTLM Restrictions

NTLM authentication can be audited and progressively
restricted.

### Host Firewall Rules

Firewall rules can restrict unnecessary administrative
connections between workstations and other systems.

### Network Segmentation

Segmentation limits which systems can communicate with
each other and helps isolate Domain Controllers and
sensitive servers.

### Privileged Access Workstations

PAWs provide dedicated hardened systems for privileged
administration and help keep high-value credentials away
from lower-value hosts.

## Key Takeaways

Lateral movement is an iterative process rather than a
single attack.

The important cycle is:

    Move
      ↓
    Harvest
      ↓
    Move Again
      ↓
    Harvest Again

A single compromised host can provide credentials,
authentication material or network access that enables the
next stage of the attack.

## Final Takeaway

The room demonstrates how an attacker can progress from an
initial foothold to the Domain Controller by combining
remote execution, credential reuse and pivoting.

The main progression is:

    Initial Foothold
          ↓
    Remote Execution
          ↓
    Credential Harvesting
          ↓
    Pass-the-Hash
          ↓
    Further Lateral Movement
          ↓
    Network Pivot
          ↓
    Domain Controller

Understanding this chain is essential for identifying both
offensive lateral movement opportunities and the defensive
controls required to break them.