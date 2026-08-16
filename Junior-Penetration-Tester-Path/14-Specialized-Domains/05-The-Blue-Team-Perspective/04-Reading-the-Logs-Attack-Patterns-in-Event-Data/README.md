# 04 - Reading the Logs: Attack Patterns in Event Data

## Overview

Detecting attacks requires understanding what normal activity looks like and recognising deviations from that baseline.

This task focuses on Windows, web, and network events and demonstrates how common attack patterns appear in logs.

---

## Important Windows Events

### Event ID 4625

Failed logon.

Useful for identifying:

    Brute Force
    Password Guessing
    Authentication Abuse

---

### Event ID 4624

Successful logon.

Useful when correlating successful authentication with previous failed attempts.

---

### Event ID 4688

New process created.

Useful for identifying:

    Suspicious Processes
    Command Execution
    Post-Exploitation Activity

---

### Event ID 7045

New service installed.

This can indicate:

    PsExec
    Malware
    Ransomware
    Persistence

---

### Event ID 1102

Security audit log was cleared.

This can be relevant to defence evasion.

---

## Detecting Network Attack Patterns

Example:

    index=botsv1 sourcetype=fgt_utm subtype=ips
    | stats count by srcip

This aggregates IPS events by source IP.

A large number of attack signatures from one source may indicate automated activity.

---

## Detecting Failed Logons

A Windows failed-logon search:

    index=botsv1 sourcetype=WinEventLog:Security EventCode=4625
    | stats count by src_ip

Large numbers of failed authentication attempts can indicate brute-force activity.

---

## Detecting Web Directory Brute-Forcing

The IIS sourcetype uses W3C-style field names.

For example:

    index=botsv1 sourcetype=iis sc_status=404
    | stats count by c_ip
    | where count > 100

A large number of 404 responses from one client can indicate directory enumeration or brute-forcing.

---

## Detecting New Services

Search for Event ID 7045:

    index=botsv1 sourcetype=WinEventLog:System EventCode=7045
    | table _time, Service_Name, Service_File_Name

Investigate unusual service names and executable paths.

Particular attention should be given to services created outside normal maintenance activity.

---

## Know Normal to See Abnormal

Detection depends on understanding legitimate activity.

The same event can have different meanings depending on:

    Frequency
    Timing
    Source
    Destination
    User
    Process
    Context

A good analyst therefore combines event data with context rather than investigating isolated events.

---

## Connecting the Dots

Individual indicators can reveal different stages of an attack:

    Authentication Events
          ↓
    Network Activity
          ↓
    Web Enumeration
          ↓
    Process Creation
          ↓
    Service Installation

Correlation helps reconstruct the attack rather than viewing each event separately.

---

## Key Takeaways

- Event IDs provide useful indicators of attacker behaviour.
- 4625 can indicate failed authentication.
- 4624 can show successful authentication.
- 4688 records process creation.
- 7045 records new service installation.
- 1102 records security log clearing.
- Web 404 patterns can reveal directory enumeration.
- Network IPS events can reveal automated attack activity.
- Context and correlation are essential for accurate detection.