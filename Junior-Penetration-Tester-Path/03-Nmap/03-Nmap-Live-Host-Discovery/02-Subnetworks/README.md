# Subnetworks

## Overview

Networks are commonly divided into smaller segments called **subnets**. Subnetting improves network organization, reduces broadcast traffic, and allows more efficient host discovery during reconnaissance.

Understanding subnet boundaries helps penetration testers define scan ranges and avoid scanning unnecessary IP addresses.

---

## Learning Objectives

- Understand what a subnet is
- Learn CIDR notation
- Identify network and host portions of an IP address
- Determine scan ranges

---

## What is a Subnet?

A subnet is a smaller logical network created from a larger IP network.

Example:

```
192.168.1.0/24
```

- Network Address: `192.168.1.0`
- Broadcast Address: `192.168.1.255`
- Usable Hosts: `192.168.1.1 – 192.168.1.254`

---

## CIDR Notation

CIDR (Classless Inter-Domain Routing) defines how many bits belong to the network.

| CIDR | Subnet Mask | Usable Hosts |
|------|-------------|-------------:|
| /30 | 255.255.255.252 | 2 |
| /29 | 255.255.255.248 | 6 |
| /28 | 255.255.255.240 | 14 |
| /24 | 255.255.255.0 | 254 |
| /16 | 255.255.0.0 | 65,534 |

---

## Example

```
10.10.10.0/30

10.10.10.0  -> Network
10.10.10.1  -> Host
10.10.10.2  -> Host
10.10.10.3  -> Broadcast
```

---

## Why It Matters

Knowing subnet boundaries allows you to:

- Define accurate scan targets
- Reduce unnecessary traffic
- Improve scan performance
- Avoid scanning invalid addresses

---

## Common Nmap Targets

Single host

```bash
nmap 10.10.10.5
```

Subnet

```bash
nmap 10.10.10.0/24
```

Multiple hosts

```bash
nmap 10.10.10.5 10.10.10.10
```

IP range

```bash
nmap 10.10.10.1-100
```

---

## Skills Practiced

- Network Fundamentals
- Subnetting
- Target Enumeration

## Key Takeaways

- Subnets divide networks into smaller segments.
- CIDR notation defines network size.
- Understanding subnet ranges helps perform faster and more accurate host discovery.