# Fine-Tuning Scope and Performance

## Overview

Nmap provides several options to control the scope, speed, and performance of a scan. Proper tuning reduces scan time while maintaining reliable results.

## Learning Objectives

- Limit the scan scope
- Control scan speed
- Optimize scan performance
- Understand timing templates

---

## Scan Specific Ports

### Scan a Single Port

```bash
nmap -p 80 <TARGET_IP>
```

### Scan Multiple Ports

```bash
nmap -p 22,80,443 <TARGET_IP>
```

### Scan a Port Range

```bash
nmap -p 1-1024 <TARGET_IP>
```

### Scan All Ports

```bash
nmap -p- <TARGET_IP>
```

---

## Fast Scan

Scan the 100 most common ports.

```bash
nmap -F <TARGET_IP>
```

---

## Sequential Port Order

Scan ports in numerical order.

```bash
nmap -r <TARGET_IP>
```

---

## Timing Templates

| Option | Description |
|---------|-------------|
| `-T0` | Paranoid |
| `-T1` | Sneaky |
| `-T2` | Polite |
| `-T3` | Normal (Default) |
| `-T4` | Aggressive |
| `-T5` | Insane |

Example:

```bash
nmap -T4 <TARGET_IP>
```

---

## Packet Rate

### Maximum Rate

```bash
nmap --max-rate 50 <TARGET_IP>
```

Limits transmission to **50 packets per second**.

### Minimum Rate

```bash
nmap --min-rate 100 <TARGET_IP>
```

Attempts to maintain at least **100 packets per second**.

---

## Parallelism

Increase the number of simultaneous probes.

```bash
nmap --min-parallelism 100 <TARGET_IP>
```

Useful for scanning large networks faster.

---

## Combining Options

```bash
sudo nmap -sS -p- -T4 --min-rate 1000 <TARGET_IP>
```

Example combines:

- SYN Scan
- All TCP Ports
- Aggressive Timing
- Minimum 1000 packets/sec

---

## Skills Practiced

- Scan Optimization
- Performance Tuning
- Efficient Enumeration

## Key Takeaways

- Limiting scan scope reduces execution time.
- Timing templates balance speed and stealth.
- Packet rate and parallelism significantly affect scan performance.
- Combining options allows Nmap to adapt to different environments.