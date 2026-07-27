# TCP Maimon Scan

## Overview

The TCP Maimon Scan is a variation of the FIN Scan that sends packets with both the **FIN** and **ACK** flags set. It was named after security researcher **Uriel Maimon**, who discovered that some BSD-based systems responded differently to this packet combination.

Like other advanced scans, it attempts to identify open ports without establishing a full TCP connection.

---

## Learning Objectives

- Understand how a Maimon Scan works
- Learn how FIN and ACK flags are used together
- Recognize operating system differences
- Interpret scan results

---

## Command

```bash
sudo nmap -sM <TARGET_IP>
```

---

## Packet Sent

```
FIN + ACK
```

---

## Expected Responses

| Response | Port State |
|-----------|------------|
| No Response | Open or Filtered |
| RST | Closed |

---

## Scan Logic

```
Client                  Target

FIN + ACK ------------->

          No Response
             OR
          <----------- RST
```

---

## Comparison

| Scan | Flags |
|------|-------|
| Null | None |
| FIN | FIN |
| Xmas | FIN + PSH + URG |
| Maimon | FIN + ACK |

---

## Advantages

- Can bypass some packet filtering rules
- Useful against certain BSD-based TCP implementations
- Generates less common traffic patterns

---

## Limitations

- Modern operating systems usually respond similarly to FIN scans
- Less reliable than SYN scanning
- Many firewalls detect or ignore these packets

---

## Skills Practiced

- Advanced TCP Scanning
- TCP Flag Analysis
- Network Enumeration

## Key Takeaways

- The Maimon Scan uses **FIN + ACK** packets.
- It behaves similarly to a FIN Scan on most modern systems.
- It is mainly useful in specific environments where TCP implementations differ.