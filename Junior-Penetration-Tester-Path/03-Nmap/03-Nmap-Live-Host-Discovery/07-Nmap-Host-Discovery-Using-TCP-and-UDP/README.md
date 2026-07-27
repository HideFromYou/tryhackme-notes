# Nmap Host Discovery Using TCP and UDP

## Overview

When ICMP is blocked, Nmap can discover hosts using TCP or UDP packets sent to specific ports.

---

## Learning Objectives

- Perform TCP discovery
- Perform UDP discovery
- Choose appropriate probe ports

---

## TCP SYN Ping

```bash
sudo nmap -PS22,80,443 -sn <TARGET>
```

---

## TCP ACK Ping

```bash
sudo nmap -PA22,80,443 -sn <TARGET>
```

---

## UDP Ping

```bash
sudo nmap -PU53,161,162 -sn <TARGET>
```

---

## Typical Responses

| Probe | Live Host Response |
|--------|-------------------|
| TCP SYN | SYN/ACK or RST |
| TCP ACK | RST |
| UDP | ICMP Port Unreachable |

---

## Advantages

- Useful when ICMP is blocked
- Can bypass some filtering rules

---

## Limitations

- Depends on available services
- Slower than ARP on local networks

---

## Skills Practiced

- TCP Discovery
- UDP Discovery
- Network Enumeration

## Key Takeaways

- TCP and UDP discovery provide alternatives to ICMP.
- Selecting common ports improves success rates.
- Multiple discovery methods increase reliability.