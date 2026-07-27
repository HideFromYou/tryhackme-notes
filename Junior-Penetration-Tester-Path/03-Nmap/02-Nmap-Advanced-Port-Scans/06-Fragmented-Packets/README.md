# Fragmented Packets

## Overview

Packet fragmentation splits IP packets into smaller fragments before transmission. Some firewalls and intrusion detection systems may have difficulty inspecting fragmented traffic.

---

## Learning Objectives

- Understand IP fragmentation
- Learn how Nmap fragments packets
- Explore firewall evasion techniques

---

## Commands

Fragment packets into 8-byte fragments:

```bash
sudo nmap -f <TARGET_IP>
```

Fragment packets into 16-byte fragments:

```bash
sudo nmap -ff <TARGET_IP>
```

---

## Why Fragment Packets?

- Bypass simple packet filters
- Reduce signature visibility
- Test firewall behavior

---

## Limitations

- Modern firewalls usually reassemble fragments.
- IDS/IPS solutions often detect fragmented scans.
- Fragmentation may slow scanning.

---

## Skills Practiced

- Firewall Evasion
- Packet Manipulation
- Advanced Reconnaissance

## Key Takeaways

- Fragmentation attempts to evade packet inspection.
- Modern security devices often mitigate this technique.
- Still useful for testing defensive controls.