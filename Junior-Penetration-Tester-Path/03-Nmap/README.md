# Nmap

Practical Nmap notes from the TryHackMe learning path, covering host discovery, port scanning, service enumeration, operating system fingerprinting, advanced scanning techniques, and reporting.

---

## Modules

| # | Module | Topics |
|---|--------|--------|
| 01 | Basic Port Scans | TCP Connect, SYN, UDP |
| 02 | Advanced Port Scans | Null, FIN, Xmas, Maimon, ACK, Window, Idle, Spoofing |
| 03 | Live Host Discovery | ARP, ICMP, TCP, UDP, Reverse DNS |
| 04 | Post Port Scans | Service Detection, OS Detection, NSE, Output |

---

## Learning Path

```
Host Discovery
      ↓
Basic Port Scanning
      ↓
Advanced Port Scanning
      ↓
Service Detection
      ↓
OS Detection
      ↓
NSE Enumeration
      ↓
Reporting
```

---

## Skills Covered

- Host Discovery
- TCP/IP Fundamentals
- Port Scanning
- Advanced Scanning Techniques
- Firewall Evasion
- Service Enumeration
- OS Fingerprinting
- Nmap Scripting Engine (NSE)
- Scan Reporting

---

## Common Commands

### Host Discovery

```bash
nmap -sn <TARGET>
```

### SYN Scan

```bash
sudo nmap -sS <TARGET>
```

### Version Detection

```bash
sudo nmap -sV <TARGET>
```

### OS Detection

```bash
sudo nmap -O <TARGET>
```

### Default NSE Scripts

```bash
sudo nmap -sC <TARGET>
```

### Full Enumeration

```bash
sudo nmap -sS -sV -O -sC <TARGET>
```

---

## Typical Pentest Workflow

```text
1. Discover live hosts
2. Scan open ports
3. Identify running services
4. Detect operating system
5. Execute NSE scripts
6. Research vulnerabilities
7. Document findings
```

---

## Repository Structure

```
Nmap/
├── README.md
├── 01-Nmap-Basic-Port-Scans/
├── 02-Nmap-Advanced-Port-Scans/
├── 03-Nmap-Live-Host-Discovery/
└── 04-Nmap-Post-Port-Scans/
```

---

## References

- Nmap Official Documentation
- TryHackMe – Nmap Learning Path
- RFC 793 (TCP)