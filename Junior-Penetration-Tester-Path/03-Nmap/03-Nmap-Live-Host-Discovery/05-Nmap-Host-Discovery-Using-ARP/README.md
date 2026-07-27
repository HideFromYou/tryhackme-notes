# Nmap Host Discovery Using ARP

## Overview

On local Ethernet networks, ARP is the fastest and most reliable method for discovering live hosts. Instead of using IP packets, Nmap sends ARP requests and waits for ARP replies.

---

## Learning Objectives

- Understand ARP discovery
- Perform ARP scans
- Recognize local network limitations

---

## Command

```bash
sudo nmap -PR -sn 192.168.1.0/24
```

---

## How It Works

```
Who has 192.168.1.10?

        ↓

ARP Reply

↓

Host is online
```

---

## Advantages

- Very fast
- Highly reliable
- Cannot be blocked by host firewalls

---

## Limitations

- Works only on the local subnet
- Not usable across routers

---

## Skills Practiced

- Local Network Enumeration
- ARP Analysis
- Host Discovery

## Key Takeaways

- ARP is Nmap's preferred method on local networks.
- Every ARP reply confirms a live host.
- ARP discovery is faster than ICMP in local environments.