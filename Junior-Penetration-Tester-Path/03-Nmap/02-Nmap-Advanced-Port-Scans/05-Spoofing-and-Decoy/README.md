# Spoofing and Decoy

## Overview

Spoofing and Decoy techniques help disguise the source of an Nmap scan, making attribution more difficult during reconnaissance.

---

## Learning Objectives

- Learn IP spoofing
- Learn MAC spoofing
- Use decoy scans
- Understand scan anonymity

---

# IP Spoofing

Spoof the source IP address.

```bash
sudo nmap -S <SPOOFED_IP> <TARGET_IP>
```

---

# MAC Address Spoofing

```bash
sudo nmap --spoof-mac <MAC> <TARGET_IP>
```

Random MAC:

```bash
sudo nmap --spoof-mac 0 <TARGET_IP>
```

---

# Decoy Scan

Generate traffic from multiple IP addresses.

```bash
nmap -D DECOY1,DECOY2,ME <TARGET_IP>
```

Random decoys:

```bash
nmap -D RND:10,ME <TARGET_IP>
```

---

## Advantages

- Makes attribution more difficult
- Can confuse basic IDS logging
- Useful during reconnaissance

---

## Limitations

- Does not guarantee anonymity
- Advanced IDS/IPS can still detect the real source

---

## Skills Practiced

- Reconnaissance
- Scan Obfuscation
- Firewall Evasion

## Key Takeaways

- Spoofing modifies source information.
- Decoys generate misleading scan traffic.
- These techniques supplement—not replace—operational security.