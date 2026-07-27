# TCP Connect Scan

## Overview

A TCP Connect Scan (`-sT`) performs the complete TCP Three-Way Handshake to determine whether a port is open. It is the default scan when Nmap cannot send raw packets.

## Learning Objectives

- Understand TCP Connect scans
- Learn how the Three-Way Handshake is used
- Identify advantages and disadvantages

## Command

```bash
nmap -sT <TARGET_IP>
```

## Scan Process

```
Client                    Server

SYN      ------------->

         <------------- SYN-ACK

ACK      ------------->

Connection Established

RST      ------------->

Connection Closed
```

## Port Responses

### Open Port

```
SYN
<-- SYN-ACK
ACK
```

### Closed Port

```
SYN
<-- RST
```

## Advantages

- Does not require root privileges
- Reliable results
- Works on most operating systems

## Disadvantages

- Slower than SYN Scan
- Fully establishes the connection
- Easier to detect in logs

## Skills Practiced

- TCP Enumeration
- Port Scanning
- Service Discovery

## Key Takeaways

- TCP Connect Scan completes the full handshake.
- It is reliable but less stealthy.
- Useful when raw packet access is unavailable.