# 05 - When Things Go Wrong: The Incident Response Lifecycle

## Overview

Incident Response (IR) provides a structured process for managing security incidents.

The lifecycle covered in this task provides defenders with a repeatable approach to:

    Prepare
    Detect
    Analyse
    Contain
    Eradicate
    Recover
    Review

---

## Incident Response Lifecycle

### 1. Preparation

Organisations prepare before an incident occurs.

This includes:

    Policies
    Procedures
    Tools
    Training
    Logging
    Response Plans

---

### 2. Detection and Analysis

Security events are identified and investigated.

This is where skills from the previous task become important:

    SIEM
    Log Analysis
    Event IDs
    Correlation
    Threat Detection

The goal is to determine whether suspicious activity represents a real incident.

---

### 3. Containment

Once an incident is confirmed, the organisation limits the attacker's access.

Examples include:

    Isolating Systems
    Blocking Traffic
    Disabling Accounts
    Restricting Access

The objective is to prevent further damage.

---

### 4. Eradication

The cause of the compromise is removed.

This can include:

    Removing Malware
    Removing Persistence
    Resetting Credentials
    Patching Vulnerabilities

---

### 5. Recovery

Systems are returned to normal operation.

Recovery should include monitoring to ensure that the attacker has not returned.

---

### 6. Post-Incident Activity

The organisation reviews the incident.

Questions include:

    What happened?
    ↓
    Why did it happen?
    ↓
    What worked?
    ↓
    What failed?
    ↓
    What should change?

The lessons learned should improve future security.

---

## The Lifecycle Is Continuous

Post-incident activity feeds back into preparation.

    Preparation
        ↓
    Detection & Analysis
        ↓
    Containment
        ↓
    Eradication
        ↓
    Recovery
        ↓
    Post-Incident Activity
        ↓
    Improved Preparation

The process is therefore continuous rather than a one-time sequence.

---

## Case Studies

The room uses real incidents to demonstrate how failures in detection and response can have major consequences.

The Target breach demonstrates the impact of alert fatigue and failure to escalate a genuine detection.

The SolarWinds incident demonstrates the importance of detection, analysis, and long-term investigation of sophisticated compromises.

---

## Detection Example

The BOTSv1 dataset can be used to investigate Event ID 1102:

    index=botsv1 sourcetype=WinEventLog:Security EventCode=1102

Event ID 1102 indicates that the security audit log was cleared.

This can be relevant to defence evasion and should be investigated in context.

---

## Pentester Perspective

Understanding the IR lifecycle helps a pentester scope engagements responsibly.

Every confirmed incident can trigger:

    Detection
    ↓
    Analysis
    ↓
    Containment
    ↓
    Eradication
    ↓
    Recovery
    ↓
    Post-Incident Review

A pentester should therefore understand the potential operational impact of testing activity.

---

## Key Takeaways

- Incident Response provides a structured process for handling security incidents.
- Preparation happens before incidents occur.
- Detection and Analysis establish what happened.
- Containment limits further damage.
- Eradication removes the cause of compromise.
- Recovery restores systems.
- Post-incident activity improves future security.
- The lifecycle feeds lessons learned back into preparation.