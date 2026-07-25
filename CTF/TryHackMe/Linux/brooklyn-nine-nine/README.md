# Brooklyn Nine-Nine - TryHackMe

## Overview

Brooklyn Nine-Nine is a beginner-friendly Linux room that introduces network enumeration, service discovery, credential identification, and Linux privilege escalation. The room encourages a structured penetration testing methodology from reconnaissance to root access.

## Objectives

* Perform service enumeration.
* Identify exposed credentials.
* Obtain initial access.
* Escalate privileges.
* Capture the user and root flags.

## Skills Learned

* Nmap enumeration
* Service enumeration
* SSH access
* Linux privilege escalation
* Sudo enumeration
* Credential discovery

## Enumeration

The assessment begins with identifying exposed network services and analysing accessible resources. Information collected during enumeration reveals the path to initial access and highlights the importance of thorough reconnaissance.

## Initial Access

After identifying valid credentials through enumeration, SSH is used to establish an initial foothold on the target system.

## Privilege Escalation

Privilege escalation focuses on identifying sudo privileges and other Linux misconfigurations that allow elevated access to the system.

## Key Takeaways

* Enumeration should always be the first priority.
* Credentials discovered during reconnaissance should be validated.
* Sudo permissions are a common Linux privilege escalation vector.
* A structured methodology improves penetration testing efficiency.

## Tools Used

* Nmap
* Gobuster
* SSH
* Netcat
* Linux CLI

---

## Disclaimer

This repository contains my personal notes and learning outcomes from TryHackMe rooms.

No flags, credentials, passwords, or complete walkthrough solutions are included.
