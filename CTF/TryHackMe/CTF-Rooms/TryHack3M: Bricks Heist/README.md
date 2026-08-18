# TryHack3M: Bricks Heist


## Overview


This room is a compromised WordPress investigation.


The target was running WordPress with the Bricks Builder theme. My goal was first to identify the initial compromise and then investigate the server to understand what the attacker had left behind.


The investigation path was:


    WordPress
        ↓
    Bricks Builder
        ↓
    CVE-2024-25600
        ↓
    RCE
        ↓
    Server Investigation
        ↓
    Cryptominer
        ↓
    Persistence
        ↓
    Miner Configuration
        ↓
    Wallet Address
        ↓
    Threat Intelligence


---


# 1. Reconnaissance


I started by identifying what was running on the target.


The web server was exposing:


    80/tcp  HTTP
    443/tcp HTTPS


The website was running WordPress and using the Bricks Builder theme.


I then researched the Bricks Builder version and found that older versions were affected by:


    CVE-2024-25600


This is an unauthenticated Remote Code Execution vulnerability.


So the initial attack path was:


    Bricks Builder
        ↓
    CVE-2024-25600
        ↓
    Unauthenticated RCE
        ↓
    Code Execution on the Server


After establishing the initial access vector, I moved on to the challenge questions and investigated the compromised machine.


---


# 2. Hidden File in the Web Directory


### Question


> What is the content of the hidden `.txt` file in the web folder?


I first inspected the web directory, including hidden files:


```bash
ls -la

Among the files I found:

650c844110baced87e1606453b93f22a.txt

I then read the file:

cat 650c844110baced87e1606453b93f22a.txt

The contents gave me the flag required for the first question.

3. Suspicious Process
Question

What is the name of the suspicious process?

Next I wanted to understand what was running on the compromised machine.

I checked the running processes:

ps aux

One process immediately stood out because it looked like a legitimate NetworkManager-related process but was running from an unusual location.

The suspicious process was:

nm-inet-dialog

The important clue here was not only the process name, but the combination of:

System-like Name
    +
Unusual Execution Path
    ↓
Suspicious Process

This suggested that the attacker was trying to masquerade the miner as a legitimate system process.

4. Persistence Mechanism
Question

What is the service name affiliated with the suspicious process?

After identifying the suspicious process, I checked the systemd services:

ls -la /etc/systemd/system/

I found a suspicious service:

ubuntu.service

This explained how the attacker could maintain persistence on the machine.

The persistence mechanism was therefore:

nm-inet-dialog
       ↓
ubuntu.service
       ↓
systemd
5. Miner Log File
Question

What is the log file name of the miner instance?

I then investigated the files under:

/lib/NetworkManager/

I found a file named:

inet.conf

This file contained information related to the cryptominer.

At this point the investigation was becoming clearer:

Suspicious Process
        ↓
Persistence Service
        ↓
Cryptominer
6. Miner Wallet Address
Question

What is the wallet address of the miner instance?

I inspected:

inet.conf

Inside the file I found an encoded string.

It was not immediately readable, so I identified it as Base64-encoded data and decoded it.

The data contained multiple layers of Base64 encoding, so I continued decoding until I reached the actual value.

The final decoded value was a Bitcoin wallet address.

The investigation path was:

inet.conf
    ↓
Base64
    ↓
Decode
    ↓
Base64
    ↓
Decode
    ↓
Bitcoin Wallet Address

This wallet address became the next useful IOC for the investigation.

7. Threat Intelligence
Question

The wallet address used has been involved in transactions between wallets belonging to which threat group?

I used the discovered Bitcoin wallet address as a threat-intelligence pivot.

The investigation showed transactions associated with:

LockBit

This connected the cryptocurrency activity found on the compromised server with infrastructure associated with the LockBit ransomware group.

8. Investigation Summary

At this point I could reconstruct what had happened on the machine.

The initial access was associated with:

CVE-2024-25600

The attacker then deployed a cryptominer.

To make the miner less obvious, the process was named:

nm-inet-dialog

Persistence was established through:

ubuntu.service

I then found the miner-related configuration/log file:

inet.conf

Inside it was encoded information which, after decoding, revealed the miner's Bitcoin wallet address.

Finally, the wallet address provided a pivot into threat intelligence and was associated with:

LockBit
Attack Chain
WordPress
    ↓
Bricks Builder
    ↓
CVE-2024-25600
    ↓
Unauthenticated RCE
    ↓
Compromised Server
    ↓
Cryptominer
    ↓
nm-inet-dialog
    ↓
ubuntu.service
    ↓
inet.conf
    ↓
Base64 Decoding
    ↓
Bitcoin Wallet
    ↓
Threat Intelligence
    ↓
LockBit
Answers
Question	Answer
Hidden .txt file	650c844110baced87e1606453b93f22a.txt
Suspicious process	nm-inet-dialog
Service	ubuntu.service
Miner log/config	inet.conf
Wallet	Bitcoin wallet discovered after decoding inet.conf
Threat group	LockBit
Key Takeaways
Start with basic reconnaissance and identify the technologies in use.
Research exposed versions when a known application is identified.
After gaining access, enumerate running processes.
Do not trust process names; investigate their execution paths.
Check systemd services when looking for persistence.
Configuration files can contain valuable malware indicators.
Encoded data should be investigated rather than ignored.
Cryptocurrency wallet addresses can be useful threat-intelligence pivots.
Individual indicators become much more useful when connected into a complete attack chain.
Final Mental Model
RECON
  ↓
IDENTIFY TECHNOLOGY
  ↓
FIND INITIAL ACCESS
  ↓
ENUMERATE COMPROMISED HOST
  ↓
IDENTIFY MALICIOUS PROCESS
  ↓
FIND PERSISTENCE
  ↓
ANALYSE MALWARE FILES
  ↓
EXTRACT IOC