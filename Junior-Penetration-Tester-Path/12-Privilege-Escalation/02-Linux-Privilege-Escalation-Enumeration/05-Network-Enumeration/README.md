# 05-Network-Enumeration/README.md

# Network Enumeration

## Overview

Network enumeration focuses on identifying the target's network configuration, active interfaces, listening services, established connections, and firewall rules.

Understanding how a host communicates with other systems can reveal hidden services, internal networks, management interfaces, and privilege escalation opportunities.

---

## Learning Objectives

- Enumerate network interfaces
- Identify listening services
- Inspect routing information
- Review active connections
- Discover firewall configuration

---

## Network Interfaces

Display interface information:

```bash
ifconfig
```

Modern systems:

```bash
ip addr
```

Useful information:

- IP addresses
- Network interfaces
- MAC addresses
- Interface status

---

## Routing Table

View routes:

```bash
ip route
```

or

```bash
route -n
```

Review:

- Default gateway
- Internal networks
- VPN interfaces

---

## Listening Services

Older systems:

```bash
netstat -tulpn
```

Modern Linux:

```bash
ss -tulpn
```

Review:

- Listening ports
- Running services
- Bound addresses

Look for:

- Internal services
- Administrative interfaces
- Unusual applications

---

## Active Connections

Display current connections:

```bash
ss -tunap
```

Useful for identifying:

- Remote management
- Database connections
- Internal communications

---

## Firewall Rules

Depending on the distribution:

```bash
iptables -L
```

or

```bash
nft list ruleset
```

Review:

- Allowed ports
- Blocked services
- Trust relationships

---

## Skills Practiced

- Interface Enumeration
- Route Enumeration
- Service Enumeration
- Connection Analysis
- Firewall Enumeration

---

## Key Takeaways

- Network enumeration identifies how the host communicates with its environment.
- Listening services frequently expose privilege escalation opportunities.
- Internal services may not be accessible externally but become reachable after initial access.
- Firewall configuration helps explain why certain services are accessible or restricted.