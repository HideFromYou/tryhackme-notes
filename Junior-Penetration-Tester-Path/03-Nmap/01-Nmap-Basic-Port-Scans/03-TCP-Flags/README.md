# TCP Flags

## Overview

TCP flags are control bits used to establish, manage, and terminate TCP connections. Nmap uses different combinations of these flags to perform various scan types and determine the state of remote ports.

## Learning Objectives

- Understand the purpose of TCP flags
- Learn the TCP connection lifecycle
- Identify how Nmap uses TCP flags
- Understand responses from target hosts

## TCP Flags

| Flag | Name | Purpose |
|------|------|---------|
| SYN | Synchronize | Initiates a connection |
| ACK | Acknowledgment | Acknowledges received data |
| FIN | Finish | Gracefully closes a connection |
| RST | Reset | Immediately terminates a connection |
| PSH | Push | Sends buffered data immediately |
| URG | Urgent | Indicates urgent data |

## TCP Three-Way Handshake

```
Client                    Server

SYN      ------------->

         <------------- SYN-ACK

ACK      ------------->
```

Connection Established

---

## Connection Termination

```
Client                    Server

FIN      ------------->

         <------------- ACK

         <------------- FIN

ACK      ------------->
```

Connection Closed

---

## How Nmap Uses TCP Flags

Different scan techniques rely on different TCP flags.

| Scan | Flags Used |
|------|------------|
| TCP Connect Scan | SYN → SYN/ACK → ACK |
| TCP SYN Scan | SYN only |
| FIN Scan | FIN |
| NULL Scan | No Flags |
| Xmas Scan | FIN + PSH + URG |

## Skills Practiced

- TCP Fundamentals
- Packet Analysis
- Nmap Scan Interpretation

## Key Takeaways

- TCP flags control every stage of a TCP connection.
- Nmap manipulates TCP flags to identify port states.
- Understanding TCP flags makes scan results easier to interpret.