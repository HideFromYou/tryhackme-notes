# Anonymous - TryHackMe

## Overview

Anonymous is a beginner-friendly Linux room focused on service enumeration, FTP and SMB assessment, initial access, and Linux privilege escalation. The challenge reinforces the importance of enumeration and demonstrates how insecure configurations can lead to full system compromise.

## Objectives

* Enumerate exposed services.
* Identify accessible resources.
* Obtain initial access.
* Escalate privileges to root.
* Complete the room objectives.

## Skills Learned

* Nmap enumeration
* FTP enumeration
* SMB enumeration
* Linux privilege escalation
* Bash scripting
* Scheduled task analysis

## Enumeration

The assessment begins with identifying open services and analysing exposed resources. Enumeration of FTP, SMB, and SSH reveals valuable information that guides the remaining attack path.

## Initial Access

Information gathered during enumeration is leveraged to obtain an initial foothold on the target system using standard Linux penetration testing techniques.

## Privilege Escalation

Privilege escalation focuses on identifying insecure configurations, writable scripts, and scheduled task execution that can be abused to obtain elevated privileges.

## Key Takeaways

* Enumeration is the foundation of every penetration test.
* Misconfigured services often expose critical attack paths.
* Scheduled tasks and writable scripts should always be inspected.
* Linux privilege escalation relies on careful system enumeration.

## Tools Used

* Nmap
* FTP
* SMBclient
* Enum4linux
* SSH
* Netcat
* Bash

---

## Disclaimer

This repository contains my personal notes and learning outcomes from TryHackMe rooms.

No flags, credentials, passwords, or complete walkthrough solutions are included.
