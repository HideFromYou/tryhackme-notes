# Idle (Zombie) Scan

## Overview

The Idle (Zombie) Scan is one of Nmap's stealthiest techniques. It performs a scan through a third-party host (the zombie), allowing the target to believe the zombie initiated the connection.

---

## Learning Objectives

- Understand Idle Scans
- Learn zombie host requirements
- Perform anonymous port scanning

---

## Command

```bash
sudo nmap -sI <ZOMBIE_IP> <TARGET_IP>
```

---

## Requirements

The zombie host should:

- Be idle
- Have predictable IP ID values
- Be reachable by both attacker and target

---

## Scan Flow

```
Attacker
     │
     ▼
Zombie
     │
     ▼
Target
```

The target never directly communicates with the attacker.

---

## Advantages

- Extremely stealthy
- Hides the attacker's IP
- Difficult to attribute

---

## Limitations

- Difficult to find suitable zombie hosts
- Rarely practical on modern networks

---

## Skills Practiced

- Anonymous Scanning
- Advanced Enumeration
- Network Reconnaissance

## Key Takeaways

- Idle Scan uses a third-party host.
- The attacker never directly contacts the target.
- It is one of Nmap's most advanced scanning techniques.