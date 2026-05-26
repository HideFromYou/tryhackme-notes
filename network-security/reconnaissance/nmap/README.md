# Nmap Reconnaissance & Enumeration Notes

Practical Nmap notes from hands-on TryHackMe training, covering host discovery, port scanning, advanced scanning techniques, service enumeration, OS fingerprinting, and the Nmap Scripting Engine (NSE).

---

## Overview

This section documents core Nmap concepts used during penetration testing.

Learning progression:

**Host Discovery → Port Scanning → Advanced Scanning → Service Enumeration → OS Detection → NSE → Reporting**

---

# 1. Live Host Discovery

## ARP Discovery
Used when operating on the same subnet / LAN.

**Command:**
```bash
nmap -PR -sn 192.168.1.0/24
```

**Concept:**
- Sends ARP requests
- Hosts that reply are alive
- Reliable for internal enumeration

**Use Case:**
Internal pentests / post-exploitation host discovery

---

## ICMP Discovery

### ICMP Echo Scan
```bash
nmap -PE -sn TARGET
```

**Concept:**
Classic ping-based host discovery using ICMP Echo Request / Reply.

---

### ICMP Timestamp Scan
```bash
nmap -PP -sn TARGET
```

**Concept:**
Requests timestamp responses instead of standard ping replies.

Useful when echo requests are filtered.

---

### ICMP Address Mask Scan
```bash
nmap -PM -sn TARGET
```

**Concept:**
Legacy ICMP discovery using subnet mask requests.

---

## TCP Host Discovery

### SYN Ping
```bash
nmap -PS22,80,443 -sn TARGET
```

Used when ICMP is blocked.

---

### ACK Ping
```bash
nmap -PA22,80,443 -sn TARGET
```

Alternative host discovery / firewall behavior testing.

---

## UDP Ping
```bash
nmap -PU53,161,162 -sn TARGET
```

UDP-based host discovery.

---

# 2. Basic Port Scanning

## TCP Connect Scan
```bash
nmap -sT TARGET
```

**Concept:**
Full TCP 3-way handshake.

Flow:
- SYN
- SYN/ACK
- ACK

**Use When:**
No elevated privileges are available.

---

## TCP SYN Scan
```bash
sudo nmap -sS TARGET
```

**Concept:**
Half-open stealth scan.

Flow:
- SYN
- SYN/ACK
- RST

**Use When:**
Standard port scanning during pentesting.

---

## UDP Scan
```bash
sudo nmap -sU TARGET
```

**Concept:**
Detect UDP services.

Examples:
- DNS
- SNMP
- TFTP

---

# 3. Advanced Port Scanning

## Null Scan
```bash
sudo nmap -sN TARGET
```

No TCP flags set.

**Behavior:**
- Closed → RST
- No response → Open|Filtered

---

## FIN Scan
```bash
sudo nmap -sF TARGET
```

FIN flag only.

---

## Xmas Scan
```bash
sudo nmap -sX TARGET
```

Flags:
- FIN
- PSH
- URG

---

## Maimon Scan
```bash
sudo nmap -sM TARGET
```

FIN + ACK scan.

Legacy TCP behavior detection.

---

## ACK Scan
```bash
sudo nmap -sA TARGET
```

**Purpose:**
Firewall mapping.

Detects:
- Filtered
- Unfiltered

---

## Window Scan
```bash
sudo nmap -sW TARGET
```

ACK variation using TCP window behavior.

---

## Custom TCP Flags
```bash
sudo nmap --scanflags SYNFIN TARGET
```

Craft custom TCP packets.

---

# 4. Evasion & Spoofing

## Source IP Spoofing
```bash
sudo nmap -S SPOOFED_IP TARGET
```

Makes scan appear to come from another IP.

---

## MAC Spoofing
```bash
sudo nmap --spoof-mac 00:11:22:33:44:55 TARGET
```

Used on local networks only.

---

## Decoy Scan
```bash
sudo nmap -D RND,RND,ME TARGET
```

Makes attribution harder by adding fake scanning sources.

---

## Idle (Zombie) Scan
```bash
sudo nmap -sI ZOMBIE_IP TARGET
```

Stealth scan through a third-party idle host.

Uses IP ID analysis.

---

## Fragmentation
8-byte fragmentation:
```bash
-f
```

16-byte fragmentation:
```bash
-ff
```

Used for simple evasion techniques.

---

## Source Port Manipulation
```bash
--source-port 53
```

Makes traffic appear to come from a trusted port.

---

## Packet Padding
```bash
--data-length 100
```

Appends random data for obfuscation.

---

# 5. Post-Port Enumeration

## Service Version Detection
```bash
nmap -sV TARGET
```

Variants:
```bash
--version-light
--version-all
```

Detect running services and versions.

---

## OS Detection
```bash
nmap -O TARGET
```

TCP/IP fingerprinting for operating system detection.

---

## Traceroute
```bash
nmap --traceroute TARGET
```

Maps packet route to target.

---

# 6. Nmap Scripting Engine (NSE)

## Default Scripts
```bash
nmap -sC TARGET
```

Equivalent:
```bash
nmap --script=default TARGET
```

---

## Specific Script
```bash
nmap --script http-date TARGET
```

Examples:
- http-title
- http-robots.txt
- ssh2-enum-algos
- vuln checks

---

## Script Categories
Examples:
- safe
- vuln
- auth
- brute
- discovery
- exploit
- malware

---

# 7. Output & Reporting

## Explain Results
```bash
--reason
```

Shows why Nmap reached its conclusions.

---

## Verbose Output
```bash
-v
-vv
```

More scan visibility.

---

## Debug Mode
```bash
-d
-dd
```

Detailed internal debugging output.

---

## Save Results

Normal:
```bash
-oN scan.txt
```

Grepable:
```bash
-oG scan.grep
```

XML:
```bash
-oX scan.xml
```

All formats:
```bash
-oA results
```

---

# Typical Pentest Workflow

```bash
nmap -sn TARGET_RANGE
sudo nmap -sS TARGET
sudo nmap -sS -sV -O -sC TARGET
```

If filtering is encountered:
- ACK scans
- Null / FIN / Xmas
- fragmentation
- decoys

---

# Key Takeaways

- Identify live hosts first
- SYN scans are the standard default
- UDP requires separate enumeration
- Advanced scans help with filtering analysis
- NSE improves enumeration significantly
- Service and OS detection support exploitation planning
- Save results for reporting
