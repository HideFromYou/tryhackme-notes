# Nmap Reconnaissance & Enumeration Foundations

Practical Nmap notes and reconnaissance methodology from hands-on TryHackMe training, covering host discovery, port scanning, advanced scan techniques, service enumeration, OS fingerprinting, and NSE scripting.

---

## Overview

This repository documents foundational Nmap concepts used in penetration testing workflows, from identifying live hosts to performing advanced enumeration and post-scan analysis.

Progression followed:

Host Discovery → Port Scanning → Advanced Scanning → Service Enumeration → OS Detection → NSE Scripting → Result Reporting

---

# 1. Live Host Discovery

Goal:

Identify which systems are online before wasting time scanning inactive hosts.

## ARP Discovery (Internal Networks)

Used when operating on the same subnet / LAN.

Command:

```bash
nmap -PR -sn 192.168.1.0/24
```

Concept:

- Sends ARP requests
- Hosts that reply are alive
- Highly reliable internally
- Common in post-exploitation internal enumeration

Use case:

Internal pentest / lateral movement reconnaissance

---

## ICMP Discovery

Used for remote host discovery.

### ICMP Echo Scan

```bash
nmap -PE -sn TARGET
```

Uses:

- ICMP Echo Request (Type 8)
- Echo Reply (Type 0)

Concept:

Classic ping-based host discovery.

---

### ICMP Timestamp Scan

```bash
nmap -PP -sn TARGET
```

Concept:

Requests system timestamp instead of standard echo response.

Useful when Echo requests are filtered.

---

### ICMP Address Mask Scan

```bash
nmap -PM -sn TARGET
```

Concept:

Legacy ICMP discovery using subnet mask requests.

---

## TCP Host Discovery

### SYN Ping

```bash
nmap -PS22,80,443 -sn TARGET
```

Used when ICMP filtering exists.

---

### ACK Ping

```bash
nmap -PA22,80,443 -sn TARGET
```

Firewall behavior analysis / alternative host discovery.

---

## UDP Ping

```bash
nmap -PU53,161,162 -sn TARGET
```

Used for UDP-based discovery.

---

# 2. Basic Port Scanning

Goal:

Determine which services are exposed.

---

## TCP Connect Scan

```bash
nmap -sT TARGET
```

Concept:

Full TCP 3-way handshake.

Flow:

SYN → SYN/ACK → ACK

Best when raw socket privileges are unavailable.

Pros:

- Reliable
- Works without sudo

Cons:

- Noisy
- Easier to detect

---

## TCP SYN Scan

```bash
sudo nmap -sS TARGET
```

Concept:

Half-open stealth scan.

Flow:

SYN → SYN/ACK → RST

Pros:

- Fast
- Standard pentest scan
- Less noisy

Cons:

Requires elevated privileges.

---

## UDP Scan

```bash
sudo nmap -sU TARGET
```

Concept:

Scans UDP services.

Examples:

- DNS
- SNMP
- TFTP

Known downside:

Slow and noisy.

---

# 3. Advanced Port Scanning

Goal:

Evasion, deception, firewall behavior analysis.

---

## Null Scan

```bash
sudo nmap -sN TARGET
```

Flags set:

None

Behavior:

- Closed → RST
- No reply → open|filtered

---

## FIN Scan

```bash
sudo nmap -sF TARGET
```

Flags:

FIN

Behavior:

- Closed → RST
- Silence → open|filtered

---

## Xmas Scan

```bash
sudo nmap -sX TARGET
```

Flags:

FIN + PSH + URG

Behavior:

Same inference model as FIN/Null.

---

## Maimon Scan

```bash
sudo nmap -sM TARGET
```

Flags:

FIN + ACK

Niche scan based on legacy TCP behavior.

---

## ACK Scan

```bash
sudo nmap -sA TARGET
```

Purpose:

Firewall mapping

Used to distinguish:

- filtered
- unfiltered

Not direct open-port discovery.

---

## Window Scan

```bash
sudo nmap -sW TARGET
```

Variation of ACK scan using TCP window behavior.

---

## Custom TCP Flags

```bash
sudo nmap --scanflags SYNFIN TARGET
```

Craft custom TCP scans.

---

# 4. Spoofing & Evasion

## Source IP Spoofing

```bash
sudo nmap -S SPOOFED_IP TARGET
```

Purpose:

Appear as another host.

Limitations:

Responses go to spoofed IP.

---

## MAC Spoofing

```bash
sudo nmap --spoof-mac 00:11:22:33:44:55 TARGET
```

Internal network only.

---

## Decoy Scan

```bash
sudo nmap -D RND,RND,ME TARGET
```

Purpose:

Confuse SIEM / attribution.

---

## Idle (Zombie) Scan

```bash
sudo nmap -sI ZOMBIE_IP TARGET
```

Purpose:

Stealth scan through third-party idle host.

Uses:

IP ID analysis.

---

## Packet Fragmentation

8-byte fragments:

```bash
-f
```

16-byte fragments:

```bash
-ff
```

---

## Source Port Manipulation

```bash
--source-port 53
```

Useful for bypassing weak filtering.

---

## Random Packet Padding

```bash
--data-length 100
```

Obfuscation / signature evasion.

---

# 5. Post Port Enumeration

## Service Version Detection

```bash
nmap -sV TARGET
```

Variants:

```bash
--version-light
--version-all
```

---

## OS Detection

```bash
nmap -O TARGET
```

TCP/IP fingerprinting.

---

## Traceroute

```bash
nmap --traceroute TARGET
```

Packet path analysis.

---

# 6. Nmap Scripting Engine (NSE)

Default scripts:

```bash
nmap -sC TARGET
```

Specific script:

```bash
nmap --script http-date TARGET
```

Examples:

- ssh2-enum-algos
- http-robots.txt
- http-title
- vuln checks
- brute force scripts

Categories:

- safe
- vuln
- auth
- brute
- discovery
- exploit
- malware

---

# 7. Useful Output Options

Reasoning:

```bash
--reason
```

Verbose:

```bash
-v
-vv
```

Debug:

```bash
-d
-dd
```

Save normal:

```bash
-oN scan.txt
```

Save grepable:

```bash
-oG scan.grep
```

Save XML:

```bash
-oX scan.xml
```

Save all:

```bash
-oA results
```

---

# Practical Pentesting Workflow

Typical approach:

```bash
nmap -sn TARGET_RANGE
sudo nmap -sS TARGET
sudo nmap -sS -sV -O -sC TARGET
```

If filtered:

- ACK scan
- Null/FIN/Xmas
- fragmentation
- decoys

---

# Key Takeaways

- Discover hosts before scanning
- SYN scan is the standard default
- UDP requires separate enumeration
- Weird scans help against weak filtering
- NSE dramatically improves enumeration
- Service + OS detection matter for exploitation
- Save scan results for reporting

---

# Skills Developed

- Network reconnaissance
- Host discovery
- Port enumeration
- Firewall behavior analysis
- Traffic deception concepts
- Service fingerprinting
- OS detection
- Script-assisted enumeration
- Scan result reporting
