# Nmap Host Discovery Using ICMP

## Overview

ICMP is commonly used to determine whether a host is reachable. Nmap supports several ICMP probe types to maximize host discovery.

---

## Learning Objectives

- Learn ICMP discovery
- Compare ICMP probe types
- Understand firewall limitations

---

## ICMP Echo

```bash
sudo nmap -PE -sn 10.10.10.0/24
```

---

## ICMP Timestamp

```bash
sudo nmap -PP -sn 10.10.10.0/24
```

---

## ICMP Address Mask

```bash
sudo nmap -PM -sn 10.10.10.0/24
```

---

## Advantages

- Simple
- Fast
- Widely supported

---

## Limitations

- ICMP is frequently blocked
- Some hosts ignore ping requests

---

## Skills Practiced

- ICMP Analysis
- Host Discovery
- Network Reconnaissance

## Key Takeaways

- ICMP is one of the most common discovery methods.
- Multiple ICMP probes improve host detection.
- Firewalls may prevent ICMP responses.