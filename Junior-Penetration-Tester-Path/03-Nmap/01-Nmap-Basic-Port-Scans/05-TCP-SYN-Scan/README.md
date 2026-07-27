# TCP SYN Scan

## Overview

A TCP SYN Scan (`-sS`), also known as a **Half-Open Scan** or **Stealth Scan**, is Nmap's most popular scanning technique. Instead of completing the TCP Three-Way Handshake, it sends a SYN packet and analyzes the target's response before terminating the connection.

## Learning Objectives

- Understand how a SYN Scan works
- Learn why it is considered stealthier than a Connect Scan
- Interpret responses from target ports
- Compare SYN and Connect scans

## Command

```bash
sudo nmap -sS <TARGET_IP>
```

> Root (or Administrator) privileges are required because Nmap crafts raw packets.

---

## Scan Process

```
Client                    Server

SYN      ------------->

         <------------- SYN-ACK

RST      ------------->

Connection Aborted
```

Unlike a TCP Connect Scan, the connection is **never fully established**.

---

## Port Responses

### Open Port

```
SYN
<-- SYN-ACK
RST
```

The server is willing to establish a connection, indicating the port is **Open**.

---

### Closed Port

```
SYN
<-- RST
```

The server immediately rejects the connection.

---

### Filtered Port

```
SYN

(no response)
```

or

```
ICMP Destination Unreachable
```

A firewall or filtering device is blocking the packets.

---

## Advantages

- Faster than TCP Connect Scan
- More stealthy
- Does not complete the TCP handshake
- Generates fewer logs on many systems

---

## Disadvantages

- Requires root/administrator privileges
- Some IDS/IPS solutions can still detect it

---

## Comparison

| TCP Connect | TCP SYN |
|-------------|----------|
| Completes handshake | Stops after SYN-ACK |
| No root required | Requires root |
| Easier to detect | More stealthy |
| Slightly slower | Faster |

---

## Skills Practiced

- TCP Enumeration
- Port Scanning
- Service Discovery
- Stealth Scanning

## Key Takeaways

- TCP SYN Scan is Nmap's default and most widely used scan.
- It identifies open ports without completing the TCP connection.
- It provides a good balance between speed, accuracy, and stealth.