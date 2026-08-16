# 05 - The Blue Team Perspective

## Overview

This room introduces the defensive side of cybersecurity and shows how a Security Operations Center (SOC) detects, investigates, and responds to attacks.

The room progresses from SOC operations and SIEM investigation to log analysis, incident response, threat intelligence, and a complete investigation.

The overall workflow is:

    SOC Operations
        ↓
    SIEM
        ↓
    Log Analysis
        ↓
    Incident Response
        ↓
    Threat Intelligence
        ↓
    Investigation
        ↓
    Purple Team Perspective

---

## Learning Objectives

By completing this room, you should understand:

- How a SOC is structured.
- The responsibilities of L1, L2, and L3 analysts.
- How SOC analysts triage and escalate alerts.
- How SIEM platforms centralise security data.
- How to investigate events using Splunk.
- How common attack patterns appear in logs.
- How the Incident Response lifecycle works.
- How MITRE ATT&CK is used to classify adversary behaviour.
- How to correlate multiple data sources during an investigation.
- How Blue Team knowledge improves penetration testing.

---

# Room Structure

| Lesson | Topic |
|---|---|
| 01 | Introduction |
| 02 | Inside the SOC: How Defenders Operate |
| 03 | Your First SIEM: Navigating Splunk |
| 04 | Reading the Logs: Attack Patterns in Event Data |
| 05 | When Things Go Wrong: The Incident Response Lifecycle |
| 06 | Know Your Enemy: Threat Intelligence Basics |
| 07 | Putting It All Together: The Wayne Corp Investigation |
| 08 | Conclusion |

---

# 01 - Introduction

The room introduces the Blue Team perspective and explains why understanding defensive operations makes a penetration tester more effective.

The main areas covered are:

    SOC Operations
    SIEM
    Log Analysis
    Incident Response
    Threat Intelligence
    MITRE ATT&CK

The key idea is that a penetration test should not only consider:

    "Can I exploit this?"

but also:

    "What would the defender see?"

---

# 02 - Inside the SOC

A SOC is organised into different tiers.

### L1 - Triage Analyst

L1 analysts:

    Monitor alerts
    ↓
    Perform initial classification
    ↓
    Close false positives
    ↓
    Escalate suspicious alerts

### L2 - Incident Handler

L2 analysts perform:

    Deep Investigation
    Incident Scoping
    Containment Coordination
    Evidence Collection

### L3 - Threat Hunter / Senior Analyst

L3 analysts work proactively:

    Threat Hunting
    Advanced Forensics
    Detection Engineering
    Tool Development

The escalation model is:

    L1 → Triage
    L2 → Investigate
    L3 → Hunt / Engineer

---

## MTTD and MTTR

### MTTD

Mean Time to Detect measures the average time between initial compromise and detection.

### MTTR

Mean Time to Respond measures the average time from detection to containment.

Lower values are better.

Long attacker dwell time provides more opportunity for:

    Lateral Movement
    Privilege Escalation
    Data Exfiltration

---

## Alert Fatigue

SOC analysts may receive large volumes of alerts, many of which are false positives.

This can result in:

    Alert Flood
        ↓
    False Positives
        ↓
    Reduced Analyst Attention
        ↓
    Genuine Alert Missed

The Target breach discussed in the room demonstrates how a legitimate security alert can fail to receive the required escalation.

---

# 03 - Your First SIEM

A SIEM centralises security data from multiple sources.

Typical sources include:

    Firewalls
    Windows Systems
    Web Servers
    Network Sensors
    Applications

The room introduces Splunk and the BOTSv1 dataset.

The main index used is:

```text
index=botsv1