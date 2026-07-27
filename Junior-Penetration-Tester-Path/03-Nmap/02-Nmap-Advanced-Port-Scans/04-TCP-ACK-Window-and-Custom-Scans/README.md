# TCP ACK, Window and Custom Scans

## Overview

ACK, Window, and Custom scans are advanced Nmap techniques used to analyze firewall rules, identify packet filtering behavior, and craft custom TCP packets.

---

## Learning Objectives

- Understand ACK scans
- Learn Window scans
- Create custom TCP scans
- Analyze firewall behavior

---

# TCP ACK Scan

The ACK Scan sends packets with only the **ACK** flag set.

Unlike SYN scans, it **cannot determine whether a port is open**, but it can identify whether a firewall is filtering packets.

### Command

```bash
sudo nmap -sA <TARGET_IP>
```

### Responses

| Response | State |
|----------|-------|
| RST | Unfiltered |
| No Response / ICMP | Filtered |

---

# TCP Window Scan

Window Scan behaves similarly to ACK Scan but also examines the TCP Window Size.

### Command

```bash
sudo nmap -sW <TARGET_IP>
```

### Possible Results

| Window Size | State |
|-------------|-------|
| Non-zero | Open |
| Zero | Closed |

> Effectiveness depends on the operating system.

---

# Custom TCP Scan

Nmap allows custom TCP flag combinations.

### Command

```bash
sudo nmap --scanflags URGACKPSHRSTSYNFIN <TARGET_IP>
```

Example:

```bash
sudo nmap --scanflags SYNFIN <TARGET_IP>
```

---

## Skills Practiced

- Firewall Detection
- Advanced TCP Flag Analysis
- Custom Packet Crafting

## Key Takeaways

- ACK scans identify firewall behavior.
- Window scans rely on TCP Window Size.
- Custom scans allow complete control over TCP flags.