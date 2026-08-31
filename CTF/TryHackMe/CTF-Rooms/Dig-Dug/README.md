# Dig Dug

## Overview

This room focused on **DNS enumeration**.

The main attack chain was:

    Nmap
      ↓
    Identify the target as a DNS server
      ↓
    Identify the domain: givemetheflag.com
      ↓
    Query the DNS server for a TXT record
      ↓
    Retrieve the flag

---

## 1. Initial Enumeration

I started with an Nmap scan.

One interesting point was that port `53` did not appear in the scan results, even though the room indicated that the machine was a DNS server.

Initially, I tried some basic DNS enumeration commands but did not get useful results.

---

## 2. Understanding the DNS Target

The important realization was that I needed to enumerate the domain:

    givemetheflag.com

through the target DNS server.

With `dig`, I can specify which DNS server should answer the query using:

    @<DNS-SERVER>

The target DNS server was:

    10.10.163.7

---

## 3. TXT Record Enumeration

I queried the target DNS server for the TXT record of the domain:

    dig @10.10.163.7 givemetheflag.com TXT

The TXT record contained the flag.

### Important Syntax

    dig @<DNS-SERVER> <DOMAIN> TXT

Example:

    dig @10.10.163.7 givemetheflag.com TXT

### Observation

The important part was the `TXT` record.

I was not simply looking for a normal DNS resolution of the domain. I specifically requested the TXT record, which contained the hidden information.

---

## 4. nslookup

The same DNS server could also be queried using `nslookup`.

I used:

    nslookup

Then:

    server 10.10.163.7

And queried:

    givemetheflag.com

This demonstrated that `nslookup` can also be used to interact directly with a specific DNS server.

---

## Attack Chain

    Nmap
      ↓
    DNS server identified
      ↓
    Domain: givemetheflag.com
      ↓
    Query target DNS server
      ↓
    TXT record
      ↓
    Flag

---

## Tools Used

### Nmap

Used for initial reconnaissance and service enumeration.

### dig

Used to query the target DNS server and retrieve the TXT record:

    dig @10.10.163.7 givemetheflag.com TXT

### nslookup

Used as an alternative DNS enumeration tool:

    nslookup
    server 10.10.163.7
    givemetheflag.com

---

## Key Takeaways

- When a machine is identified as a DNS server, think about DNS queries and records.
- `dig` allows me to specify the DNS server with `@<DNS-SERVER>`.
- DNS records are not limited to A records.
- `TXT` records can contain additional information and should be checked during DNS enumeration.
- In this room, the flag was stored in the TXT record of `givemetheflag.com`.

### DNS Mental Model

    DNS Server
        ↓
    Domain
        ↓
    Record Type
        ↓
    DNS Response

Example:

    @10.10.163.7
         ↓
    givemetheflag.com
         ↓
        TXT
         ↓
       Flag