# 02 - Inside the SOC: How Defenders Operate

## Overview

A Security Operations Center (SOC) is responsible for monitoring security events, investigating suspicious activity, and responding to incidents.

The room uses the 2013 Target breach to demonstrate an important lesson:

    Technology can detect an attack
        ↓
    But people and processes must respond

Target's FireEye system detected malware, but the alert was not escalated. The failure demonstrates the importance of SOC processes and alert handling.

---

## SOC Tier Structure

### L1 - Triage Analyst

L1 analysts are the first line of defence.

Responsibilities include:

    Monitor alert queue
    ↓
    Perform initial classification
    ↓
    Close false positives
    ↓
    Escalate suspicious alerts

L1 handles the highest volume of alerts.

If deeper investigation is required, the alert is escalated.

---

### L2 - Incident Handler

L2 receives escalated alerts from L1.

Responsibilities include:

    Deep-Dive Analysis
    Incident Scoping
    Containment Coordination
    Evidence Collection

L2 analysts have more experience and broader access to security tools.

---

### L3 - Threat Hunter / Senior Analyst

L3 works proactively.

Instead of waiting for alerts, L3 analysts:

    Form hypotheses
    Hunt for compromise
    Build detection rules
    Perform advanced forensics
    Develop tools

Some organisations also have an L4 level for SOC management, engineering, and platform maintenance.

---

## Escalation Flow

The basic flow is:

    L1
    Triage
      ↓
    L2
    Investigate
      ↓
    L3
    Hunt / Engineer

Each tier filters the workload for the tier above it.

---

## Analyst Workflow

An L1 analyst follows a consistent workflow:

    1. Monitor the queue.

    2. Triage the alert.

    3. Investigate suspicious activity.

    4. Decide whether to close or escalate.

False positives should be documented when closed.

Suspicious alerts should be escalated with the analyst's findings attached.

---

## MTTD

Mean Time to Detect (MTTD) measures the average time between an attacker's initial compromise and the organisation detecting the breach.

Lower is better.

Long detection times provide attackers with more opportunity to:

    Move Laterally
    Escalate Privileges
    Exfiltrate Data

---

## MTTR

Mean Time to Respond (MTTR) measures the average time from detection to containment.

Detection alone is not enough.

The organisation must also contain the attacker.

---

## Alert Fatigue

SOC analysts process large numbers of alerts, many of which are false positives.

This can create:

    Alert Flood
       ↓
    Repeated False Positives
       ↓
    Reduced Analyst Attention
       ↓
    Genuine Alert Gets Missed

This is known as alert fatigue.

The Target example demonstrates how a legitimate alert can fail to receive the required attention when analysts are overwhelmed by noise.

---

## Key Takeaways

- SOCs use tiered responsibilities.
- L1 performs triage.
- L2 performs deeper investigation and containment coordination.
- L3 performs threat hunting and advanced analysis.
- MTTD measures detection time.
- MTTR measures response time.
- Lower MTTD and MTTR are better.
- Alert fatigue can cause genuine attacks to be missed.
- Effective security requires technology, people, and processes.