# 05 - Pivoting

## Overview

This task focused on pivoting through a compromised host
to reach systems and services located on a restricted
network segment.

The WebServer was used as the pivot because it could reach
the internal network containing the Domain Controller.

## Topics Covered

- Pivoting
- Network segmentation
- SSH tunnelling
- Local Port Forwarding
- Dynamic Port Forwarding
- SOCKS Proxy
- ProxyChains

## The Problem

The AttackBox could directly reach the WebServer but could
not directly reach:

- The Domain Controller
- Internal services
- The restricted subnet

The WebServer could reach those internal systems.

Therefore:

    AttackBox
        ↓
    WebServer
        ↓
    Internal Network
        ↓
    Domain Controller

## Local Port Forwarding

SSH local port forwarding creates a specific tunnel from
a local port to a destination accessible from the pivot.

Example:

    ssh -L <LOCAL_PORT>:<INTERNAL_IP>:<DEST_PORT> \
    <USER>@<PIVOT_IP> -N

The local machine listens on `<LOCAL_PORT>`.

Traffic is forwarded through the SSH connection to the
internal destination.

## Example

Forward RDP through the WebServer:

    ssh -L 13389:<DC_IP>:3389 <USER>@<PIVOT_IP> -N

Then connect locally:

    xfreerdp /v:127.0.0.1:13389 /u:<USERNAME>

The Domain Controller sees the connection as coming from
the pivot host.

## Dynamic Port Forwarding

Dynamic forwarding creates a SOCKS proxy.

Example:

    ssh -f -D 1080 <USER>@<PIVOT_IP> -N

This creates a SOCKS proxy on:

    127.0.0.1:1080

Unlike local forwarding, dynamic forwarding can be used
for multiple destinations.

## ProxyChains

ProxyChains can force supported TCP traffic through the
SOCKS proxy.

Configure:

    /etc/proxychains.conf

Example:

    [ProxyList]
    socks4 127.0.0.1 1080

Then run commands through ProxyChains:

    proxychains <COMMAND>

## Local vs Dynamic Forwarding

### Local Forwarding

    AttackBox
        ↓
    Local Port
        ↓
    SSH Tunnel
        ↓
    One Internal Service

Best when accessing one specific service.

### Dynamic Forwarding

    AttackBox
        ↓
    SOCKS Proxy
        ↓
    SSH Tunnel
        ↓
    Multiple Internal Hosts / Ports

Useful for broader internal network access.

## Key Takeaways

Pivoting allows an attacker to use a compromised host as
a network relay.

The main idea is:

    Cannot Reach Target Directly
              ↓
    Find Compromised Host With Access
              ↓
    Create Tunnel
              ↓
    Route Traffic Through Pivot
              ↓
    Reach Internal Target