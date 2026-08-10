# 02 - Mapping Out the Network

## Overview

In this task, we mapped the target network to identify live
hosts, discover running services and determine which host
was the Domain Controller.

We started with a subnet provided as part of the penetration
testing scope and performed host discovery before moving on
to port and service enumeration.

## Topics Covered

- Host discovery
- ICMP
- fping
- Nmap
- Ping scanning
- Port scanning
- Service version detection
- Nmap NSE scripts
- Domain Controller identification
- Full TCP port scanning

## Host Discovery

The first step was to identify all live hosts within the
target subnet.

### fping

`fping` can send ICMP requests to multiple hosts and can
accept an entire subnet as input.

Command:

    fping -agq <SUBNET>

### Options

    -a    Show systems that are alive
    -g    Generate a target list from the supplied network
    -q    Quiet mode

After discovering the live hosts, the relevant IP addresses
can be stored in a file for later scans.

Example:

    cat hosts.txt

    <HOST_IP_1>
    <HOST_IP_2>

## Nmap Host Discovery

Nmap can also be used to discover live hosts without
performing a port scan.

Command:

    nmap -sn <SUBNET>

### Option

    -sn    Ping scan to determine which hosts are up
           without port scanning

## Port Scanning

After discovering live hosts, the next objective is to
identify the Domain Controller.

Important Active Directory ports include:

| Port | Protocol | Purpose |
|---:|---|---|
| 88 | Kerberos | Kerberos authentication |
| 135 | MS-RPC | RPC enumeration |
| 139 | SMB/NetBIOS | Legacy SMB access |
| 389 | LDAP | Active Directory queries |
| 445 | SMB | Modern SMB access |
| 464 | Kerberos/kpasswd | Password-related Kerberos service |

## Service Version Scan

We can scan the relevant AD ports using:

    nmap -p 88,135,139,389,445 -sV -sC -iL hosts.txt

### Options

    -sV    Enable service/version detection
    -sC    Run Nmap default NSE scripts
    -iL    Read targets from hosts.txt

## Identifying the Domain Controller

A Domain Controller can often be identified by the presence
of several Active Directory-related services.

Typical indicators include:

    88    Kerberos
    389   LDAP
    445   SMB

Service banners may also reveal:

- Windows Server
- Domain names
- Active Directory-related information

## Full Port Scan

For a more exhaustive assessment, all TCP ports can be scanned:

    nmap -sS -p- -T3 -iL hosts.txt -oN full_port_scan.txt

### Options

    -sS    TCP SYN scan
    -p-    Scan all 65,535 TCP ports
    -T3    Normal timing template
    -iL    Read targets from hosts.txt
    -oN    Save output to a file

A full port scan helps identify critical services running
on non-standard ports.

## Enumeration Workflow

The overall process was:

    Target Subnet
          ↓
    Host Discovery
          ↓
    Live Hosts
          ↓
    Port Scanning
          ↓
    Service Detection
          ↓
    Identify Domain Controller
          ↓
    Further AD Enumeration

## Key Takeaways

The first stage of an Active Directory assessment is to
understand the network.

The main objectives are:

- Identify live hosts
- Identify open ports
- Identify running services
- Locate the Domain Controller
- Identify the Active Directory domain
- Prepare the targets for further enumeration