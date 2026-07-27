# Summary

## Host Discovery Methods

| Method | Command |
|---------|---------|
| ARP | `-PR -sn` |
| ICMP Echo | `-PE -sn` |
| ICMP Timestamp | `-PP -sn` |
| ICMP Address Mask | `-PM -sn` |
| TCP SYN | `-PS -sn` |
| TCP ACK | `-PA -sn` |
| UDP | `-PU -sn` |

---

## Useful Options

| Option | Purpose |
|---------|---------|
| `-sn` | Host discovery only |
| `-PR` | ARP discovery |
| `-PE` | ICMP Echo |
| `-PP` | ICMP Timestamp |
| `-PM` | ICMP Address Mask |
| `-PS` | TCP SYN Ping |
| `-PA` | TCP ACK Ping |
| `-PU` | UDP Ping |
| `-R` | Reverse DNS lookup |
| `-n` | Disable DNS resolution |

---

## Skills Developed

- Host Discovery
- Network Enumeration
- TCP/IP Fundamentals
- DNS Reconnaissance

## Key Takeaways

- Always identify live hosts before port scanning.
- ARP is preferred on local networks.
- ICMP, TCP, and UDP provide alternative discovery methods.
- Reverse DNS can reveal valuable information about target systems.