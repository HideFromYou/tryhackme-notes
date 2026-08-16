# 07 - Putting It All Together: The Wayne Corp Investigation

## Overview

The Wayne Corp investigation combines the skills learned throughout the room into a single SOC investigation.

The investigation follows an alert and reconstructs the attack by correlating multiple data sources in Splunk.

---

## Investigation Flow

    Alert
      ↓
    Triage
      ↓
    Network Investigation
      ↓
    Web Investigation
      ↓
    Reconnaissance Confirmation
      ↓
    Windows Event Investigation
      ↓
    Attack Chain Reconstruction

---

## Step 1 - Triage the Alert

Start with the Suricata data source.

Use:

    index=botsv1 sourcetype=suricata NOT src_ip=192.168.* NOT src_ip=10.*
    | stats count by src_ip

The goal is to identify the suspicious external source IP.

---

## Step 2 - Pivot to Web Access Logs

Use the attacker IP identified during triage.

Search IIS logs:

    index=botsv1 sourcetype=iis c_ip=<attacker_ip> cs_method=POST
    | stats count by cs_uri_stem

This identifies the endpoints targeted by the attacker.

---

## Step 3 - Confirm Reconnaissance

Investigate HTTP responses from the attacker.

Use:

    index=botsv1 sourcetype=iis c_ip=<attacker_ip> sc_status=404
    | stats count

A high number of 404 responses can indicate web directory enumeration.

This connects the investigation with the attack patterns studied earlier.

---

## Step 4 - Check Windows Event Logs

Search for authentication events associated with the attacker IP:

    index=botsv1 sourcetype=WinEventLog:Security (EventCode=4624 OR EventCode=4625) <attacker_ip>
    | stats count by EventCode

This can reveal:

    Failed Logons
    Successful Logons

The attacker IP is used to correlate activity across different data sources.

---

## Reconstructing the Attack Chain

The investigation connects multiple sources:

    Suricata
       ↓
    IIS
       ↓
    Windows Security Logs

The resulting investigation can show a sequence such as:

    Network Activity
          ↓
    Web Reconnaissance
          ↓
    Authentication Activity
          ↓
    Post-Exploitation Evidence

---

## Cross-Sourcetype Correlation

Each stage of the investigation uses a different sourcetype.

    suricata
    iis
    WinEventLog:Security

Correlation allows the analyst to reconstruct activity that would not be obvious from a single log source.

---

## Incident Response Context

The investigation represents the:

    Detection and Analysis

phase of the Incident Response lifecycle.

After confirmation, defenders would move toward:

    Containment
        ↓
    Eradication
        ↓
    Recovery
        ↓
    Post-Incident Activity

---

## ATT&CK Context

The investigation can also be mapped to ATT&CK techniques based on the observed behaviour.

This connects:

    SIEM Evidence
        ↓
    Attack Technique
        ↓
    ATT&CK Mapping
        ↓
    Detection / Reporting

---

## Pentester Perspective

This investigation demonstrates why understanding Blue Team operations improves penetration testing.

A pentester can ask:

    What would the SOC see?
    ↓
    Which logs would contain my activity?
    ↓
    Which Event IDs would appear?
    ↓
    Could defenders correlate my actions?
    ↓
    What evidence would remain?

This helps evaluate both attack effectiveness and defensive visibility.

---

## Key Takeaways

- Start with the alert.
- Identify the suspicious source.
- Pivot across relevant data sources.
- Use the attacker IP to correlate events.
- Investigate network, web, and Windows logs together.
- Reconstruct the attack chain.
- Map observed behaviour to ATT&CK where appropriate.
- Think about what evidence your own pentest activity would leave behind.