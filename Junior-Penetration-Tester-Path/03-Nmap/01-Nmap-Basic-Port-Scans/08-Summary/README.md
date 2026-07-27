# Summary

## Overview

This room introduced the fundamental Nmap port scanning techniques used during reconnaissance and enumeration.

## Scan Types Covered

| Scan | Command |
|------|---------|
| TCP Connect Scan | `nmap -sT <TARGET_IP>` |
| TCP SYN Scan | `sudo nmap -sS <TARGET_IP>` |
| UDP Scan | `sudo nmap -sU <TARGET_IP>` |

---

## Useful Options

| Option | Purpose |
|---------|---------|
| `-p-` | Scan all ports |
| `-p1-1023` | Scan ports 1–1023 |
| `-F` | Scan the 100 most common ports |
| `-r` | Scan ports sequentially |
| `-T0` → `-T5` | Timing templates |
| `--max-rate` | Limit packet rate |
| `--min-rate` | Set minimum packet rate |
| `--min-parallelism` | Increase parallel probes |

---

## Skills Developed

- Port Scanning
- Service Discovery
- TCP/IP Fundamentals
- Scan Optimization
- Network Enumeration

## Key Takeaways

- TCP Connect, TCP SYN, and UDP scans are the foundation of Nmap enumeration.
- Understanding TCP behavior improves scan interpretation.
- Performance tuning helps balance speed, stealth, and accuracy.
- Choosing the appropriate scan type depends on the target environment and assessment goals.