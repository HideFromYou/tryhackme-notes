# UDP Scan

## Overview

A UDP Scan (`-sU`) identifies services running over the User Datagram Protocol (UDP). Unlike TCP, UDP is connectionless, making scanning slower and more difficult to interpret.

## Learning Objectives

- Understand how UDP scanning works
- Learn how Nmap detects UDP services
- Identify common UDP ports
- Recognize UDP scan limitations

## Command

```bash
sudo nmap -sU <TARGET_IP>
```

---

## How UDP Scanning Works

```
Client                    Server

UDP Packet ------------->

        No Response
             OR
ICMP Port Unreachable <---
```

Because UDP has no handshake, Nmap relies on responses—or the lack of responses—to determine port states.

---

## Port States

| Response | State |
|----------|-------|
| UDP response received | Open |
| ICMP Port Unreachable | Closed |
| No response | Open \| Filtered |

---

## Common UDP Services

| Port | Service |
|------|---------|
| 53 | DNS |
| 67 | DHCP Server |
| 68 | DHCP Client |
| 69 | TFTP |
| 123 | NTP |
| 161 | SNMP |
| 500 | ISAKMP |
| 514 | Syslog |

---

## Advantages

- Discovers UDP services
- Identifies services often missed by TCP scans

---

## Disadvantages

- Slower than TCP scans
- More false positives
- Firewalls frequently filter UDP traffic

---

## Skills Practiced

- UDP Enumeration
- Service Discovery
- Network Reconnaissance

## Key Takeaways

- UDP scanning is slower because there is no connection handshake.
- Many important services rely on UDP.
- Combining TCP and UDP scans provides more complete enumeration.