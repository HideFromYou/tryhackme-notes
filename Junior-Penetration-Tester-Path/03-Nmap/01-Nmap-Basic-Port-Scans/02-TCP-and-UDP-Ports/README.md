# TCP and UDP Ports

## Overview

Ports allow multiple network services to communicate over a single IP address. TCP and UDP are the two primary transport layer protocols used by modern applications, each providing different communication characteristics.

## Learning Objectives

- Understand the purpose of network ports
- Differentiate between TCP and UDP
- Identify common port states
- Recognize well-known port ranges

## TCP vs UDP

| TCP | UDP |
|------|-----|
| Connection-oriented | Connectionless |
| Reliable delivery | Best-effort delivery |
| Error checking | Minimal error checking |
| Slower | Faster |

## Port Ranges

| Range | Description |
|--------|-------------|
| 0–1023 | Well-Known Ports |
| 1024–49151 | Registered Ports |
| 49152–65535 | Dynamic / Ephemeral Ports |

## Common Ports

| Port | Protocol | Service |
|------|----------|---------|
| 21 | TCP | FTP |
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |

## Skills Practiced

- Network Fundamentals
- Service Identification
- Port Enumeration

## Key Takeaways

- Ports identify individual network services.
- TCP prioritizes reliability, while UDP prioritizes speed.
- Knowing common ports helps identify running services during reconnaissance.