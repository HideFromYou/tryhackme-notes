# 06 - Know Your Enemy: Threat Intelligence Basics

## Overview

Threat Intelligence provides context about adversaries, their behaviour, and the techniques they use.

The room introduces MITRE ATT&CK and demonstrates how observed activity can be mapped to attacker techniques.

---

## TTPs

Threat intelligence commonly describes:

    Tactics
    Techniques
    Procedures

These are referred to as:

    TTPs

They describe what an adversary is trying to achieve and how they perform their actions.

---

## MITRE ATT&CK

MITRE ATT&CK provides a structured knowledge base of adversary tactics and techniques.

Observed activity can be mapped to ATT&CK techniques.

This provides a common language for:

    Detection
    Investigation
    Reporting
    Threat Intelligence

---

## Example Mapping

The room maps common activities to ATT&CK.

| Attack Pattern | ATT&CK Technique | ID |
|---|---|---|
| Port and service scanning | Network Service Discovery | T1046 |
| Command execution | Command and Scripting Interpreter | T1059 |

The exact observed behaviour should determine the technique mapping.

---

## Why ATT&CK Matters to a Pentester

Pentest findings can be described using ATT&CK techniques.

Instead of only reporting:

    "The attacker performed network scanning."

A report can identify the corresponding ATT&CK technique:

    Network Service Discovery
    T1046

This creates consistent terminology between offensive and defensive teams.

---

## Process Creation Example

The room demonstrates searching for process creation events:

    index=botsv1 sourcetype=WinEventLog:Security EventCode=4688
    | table _time, ...

Event ID 4688 records new process creation.

This activity can be mapped to:

    Command and Scripting Interpreter
    T1059

when the observed behaviour supports that classification.

---

## ATT&CK Navigator

The ATT&CK Navigator provides an interactive way to work with the ATT&CK matrix.

It can help visualise:

    Techniques
    Sub-techniques
    Adversary Behaviour
    Coverage

---

## Detection Mapping

Threat intelligence can connect attacker behaviour to detection:

    Attacker Technique
          ↓
    Observable Event
          ↓
    SIEM Query
          ↓
    Detection
          ↓
    Investigation

This makes threat intelligence useful for both SOC analysts and penetration testers.

---

## Pentester Perspective

Mapping activity to ATT&CK improves reporting.

A strong finding can contain:

    Technique
    ↓
    Evidence
    ↓
    Detection Opportunity
    ↓
    Defensive Recommendation

This gives defenders information they can directly use.

---

## Key Takeaways

- Threat intelligence provides context about adversary behaviour.
- TTPs describe tactics, techniques, and procedures.
- MITRE ATT&CK provides a structured framework for adversary techniques.
- T1046 represents Network Service Discovery.
- T1059 represents Command and Scripting Interpreter.
- ATT&CK improves communication between Red and Blue Teams.
- Pentest findings can be mapped to ATT&CK techniques.