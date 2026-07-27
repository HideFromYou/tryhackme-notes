# OS Detection and Traceroute

## Overview

Nmap can estimate the target operating system by analyzing TCP/IP responses and map the network path between the attacker and the target.

---

## Learning Objectives

- Detect operating systems
- Understand fingerprinting
- Perform traceroute

---

## OS Detection

```bash
sudo nmap -O <TARGET>
```

Nmap compares TCP/IP fingerprints against its database to estimate the operating system.

---

## Traceroute

```bash
sudo nmap --traceroute <TARGET>
```

Displays the routers (hops) between the scanner and the target.

---

## Typical Information

- Operating System
- Network Distance
- Hop Count
- TCP/IP Fingerprint

---

## Limitations

- Firewalls may alter fingerprints.
- Virtualization can reduce accuracy.
- Routers may not respond during traceroute.

---

## Skills Practiced

- OS Fingerprinting
- Network Mapping
- Reconnaissance

## Key Takeaways

- `-O` estimates the target OS.
- `--traceroute` maps the network path.
- Results should be combined with other enumeration techniques.