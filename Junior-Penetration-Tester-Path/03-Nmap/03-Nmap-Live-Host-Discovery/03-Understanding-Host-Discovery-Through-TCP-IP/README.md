# Understanding Host Discovery Through TCP/IP

## Overview

Host discovery relies on the TCP/IP protocol suite to determine whether a system is online. Nmap sends different types of network packets and analyzes the responses to identify active hosts before performing port scans.

---

## Learning Objectives

- Understand how host discovery works
- Learn the role of TCP/IP
- Interpret common network responses

---

## Host Discovery Principle

```
Probe  ----------->  Target

      <-----------  Response
```

Any valid response indicates the target is likely online.

---

## Common Responses

| Probe | Possible Response |
|--------|-------------------|
| ARP | ARP Reply |
| ICMP Echo | Echo Reply |
| TCP SYN | SYN/ACK or RST |
| TCP ACK | RST |
| UDP | ICMP Port Unreachable |

---

## Why Different Methods?

Not every network allows every protocol.

Examples:

- ICMP may be blocked
- TCP ports may be filtered
- UDP responses may be limited
- ARP only works on local networks

Nmap automatically selects the most appropriate discovery method.

---

## Skills Practiced

- TCP/IP Fundamentals
- Host Discovery
- Packet Analysis

## Key Takeaways

- Host discovery is based on packet responses.
- Different protocols reveal live hosts in different situations.
- Nmap combines multiple techniques to improve detection.