# 14 - Specialized Domains

## Overview

This section covers specialised cybersecurity domains that extend beyond the core penetration-testing methodology.

The focus is on understanding different environments, technologies, and security perspectives that a modern penetration tester may encounter during an engagement.

The section includes:

    01 - Wireless Security
    02 - Mobile Application Security
    03 - Cloud Security Fundamentals
    04 - LLM Pentesting
    05 - The Blue Team Perspective
    06 - DevSecOps Basics

Each domain introduces a different attack surface and requires a different testing mindset.

---

# 01 - Wireless Security

Wireless Security focuses on the security of Wi-Fi and wireless networks.

The main areas covered include:

    Wireless Networking
    Wi-Fi Security
    Authentication
    Encryption
    Wireless Enumeration
    Wireless Attacks
    Wireless Assessment

The goal is to understand how wireless networks are discovered, authenticated, attacked, and secured.

A wireless assessment generally follows:

    Reconnaissance
        ↓
    Network Discovery
        ↓
    Authentication Analysis
        ↓
    Security Testing
        ↓
    Attack / Weakness Validation
        ↓
    Reporting

Wireless environments introduce attack surfaces that do not exist in traditional wired networks.

---

# 02 - Mobile Application Security

Mobile Application Security focuses on identifying vulnerabilities in mobile applications and their supporting infrastructure.

The assessment can include:

    Application Analysis
    API Testing
    Authentication
    Authorisation
    Data Storage
    Network Communication
    Application Behaviour

A mobile application should not be viewed only as the application installed on the device.

The complete attack surface may include:

    Mobile Application
          ↓
    API
          ↓
    Backend
          ↓
    Database
          ↓
    External Services

Testing therefore requires understanding both the mobile client and the services it communicates with.

The general methodology is:

    Reconnaissance
        ↓
    Application Analysis
        ↓
    API Enumeration
        ↓
    Security Testing
        ↓
    Exploitation
        ↓
    Impact Assessment
        ↓
    Reporting

---

# 03 - Cloud Security Fundamentals

Cloud Security Fundamentals introduces the security concepts required when assessing cloud environments.

Cloud environments introduce additional considerations such as:

    Identity
    Access Management
    Cloud Resources
    Storage
    Networking
    APIs
    Permissions
    Secrets
    Infrastructure as Code

A cloud security assessment should consider both the resources and the identities controlling them.

The general model is:

    Identity
        ↓
    Permissions
        ↓
    Cloud Resource
        ↓
    Data / Service

Misconfigured permissions can allow an attacker to access resources that should not be available to them.

Important areas include:

    Authentication
    Authorisation
    Least Privilege
    Resource Exposure
    Storage Security
    Secrets Management
    Cloud Configuration

The key mindset is:

    What resources exist?
        ↓
    Who can access them?
        ↓
    What permissions do they have?
        ↓
    What can those permissions access?
        ↓
    Can the access be abused?

---

# 04 - LLM Pentesting

LLM Pentesting introduces the security testing of Large Language Model applications.

LLMs create a different attack surface from traditional web applications.

The attack surface can include:

    User Input
    System Prompts
    Application Logic
    APIs
    External Data
    Tools
    Plugins
    Internal Services

The main methodology is:

    Reconnaissance
        ↓
    Fingerprinting
        ↓
    System Prompt Analysis
        ↓
    Prompt Injection
        ↓
    Jailbreaking
        ↓
    Tool / Data Access
        ↓
    Impact Assessment
        ↓
    Reporting

---

## Prompt Injection

Prompt injection attempts to manipulate the instructions given to an LLM.

Two important categories are:

    Direct Prompt Injection
    Indirect Prompt Injection

Direct injection comes from user-controlled input.

Indirect injection introduces malicious instructions through external content processed by the LLM.

---

## Jailbreaking

Jailbreaking attempts to bypass the model's safety behaviour.

Testing may involve:

    Role-Playing
    Context Manipulation
    Instruction Reframing
    Multi-Step Prompting
    Input Transformation

The important question is not simply whether the model can be tricked.

The tester must determine:

    What can the model access?
        ↓
    What can the model control?
        ↓
    What is the real security impact?

---

# 05 - The Blue Team Perspective

This room introduces the defensive side of cybersecurity.

The focus is on:

    SOC Operations
    SIEM
    Log Analysis
    Incident Response
    Threat Intelligence
    MITRE ATT&CK
    Investigation
    Purple Teaming

---

## SOC

A Security Operations Center monitors and investigates security events.

Typical responsibilities are divided into:

    L1
      ↓
    Triage

    L2
      ↓
    Investigation

    L3
      ↓
    Threat Hunting / Advanced Analysis

Important operational metrics include:

    MTTD
    MTTR

Alert fatigue is also an important problem because large volumes of false positives can cause genuine alerts to receive less attention.

---

## SIEM

A SIEM centralises security data from different sources.

Examples include:

    Windows Logs
    Web Logs
    Network Logs
    Firewall Logs
    Security Sensors

The investigation workflow is:

    Collect
      ↓
    Search
      ↓
    Filter
      ↓
    Correlate
      ↓
    Investigate

---

## Log Analysis

Important Windows events include:

    4624 → Successful Logon
    4625 → Failed Logon
    4688 → Process Creation
    7045 → New Service Installed
    1102 → Security Audit Log Cleared

The important lesson is that individual events become more useful when correlated with other activity.

---

## Incident Response

The Incident Response lifecycle is:

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

---

## Threat Intelligence

Threat Intelligence provides context about adversary behaviour.

Important concepts include:

    Tactics
    Techniques
    Procedures

MITRE ATT&CK provides a common framework for describing adversary techniques.

---

## Purple Team Perspective

Red and Blue Teams can work together through a feedback loop:

    Attack
      ↓
    Detection
      ↓
    Investigation
      ↓
    Security Improvement
      ↓
    New Test

Understanding the Blue Team perspective makes penetration testing more realistic and improves reporting.

---

# 06 - DevSecOps Basics

DevSecOps focuses on integrating security into the software development lifecycle.

The evolution covered is:

    Waterfall
        ↓
    Agile
        ↓
    DevOps
        ↓
    Shift Left
        ↓
    DevSecOps

---

## Waterfall

Waterfall follows a sequential development model.

    Development
        ↓
    Testing
        ↓
    Operations
        ↓
    Delivery

This separation can create communication gaps, delays, and friction.

---

## Agile

Agile introduces greater flexibility and responsiveness to change.

The core idea is:

    Plan
      ↓
    Develop
      ↓
    Test
      ↓
    Learn
      ↓
    Adapt
      ↓
    Repeat

---

## DevOps

DevOps focuses on:

    Collaboration
    Integration
    Automation
    Continuous Feedback

Important concepts include:

    CI/CD
    Infrastructure as Code
    Configuration Management
    Orchestration
    Monitoring
    Microservices

---

## Shift Left

Shift Left means introducing security earlier in the development lifecycle.

Instead of:

    Development
        ↓
    Testing
        ↓
    Production
        ↓
    Security

security becomes integrated throughout development:

    Development
        ↓
    Security Testing
        ↓
    Testing
        ↓
    Deployment
        ↓
    Production

Finding vulnerabilities earlier can reduce:

    Risk
    Remediation Cost
    Rollbacks
    Security Bottlenecks

---

## DevSecOps Culture

DevSecOps is not only about security tools.

A successful DevSecOps culture requires:

    Autonomy
    Visibility
    Transparency
    Understanding
    Empathy
    Trust

Security should become a shared responsibility rather than a separate security silo.

---

# Cross-Domain Pentester Mindset

Although these rooms cover very different technologies, the same fundamental penetration-testing methodology can be applied.

## 1. Reconnaissance

    What exists?
    ↓
    What is exposed?
    ↓
    What technology is being used?

## 2. Enumeration

    What services?
    ↓
    What users?
    ↓
    What APIs?
    ↓
    What permissions?
    ↓
    What functionality?

## 3. Vulnerability Identification

    What is misconfigured?
    ↓
    What is vulnerable?
    ↓
    What security control can be bypassed?

## 4. Exploitation

    Can the weakness be reproduced?
        ↓
    What access does it provide?
        ↓
    Can it be chained?

## 5. Impact Assessment

    What can an attacker actually achieve?

## 6. Reporting

    Vulnerability
        ↓
    Evidence
        ↓
    Reproduction
        ↓
    Impact
        ↓
    Remediation

---

# What Changes Between Domains?

The methodology remains similar, but the attack surface changes.

| Domain | Primary Attack Surface |
|---|---|
| Wireless | Wireless networks and authentication |
| Mobile | Mobile applications and APIs |
| Cloud | Identities, permissions, resources and APIs |
| LLM | Models, prompts, applications and integrations |
| Blue Team | Detection, monitoring and response |
| DevSecOps | Development pipelines and security processes |

The tester must adapt their tools and techniques to the environment being assessed.

---

# Overall Learning Path

The six domains can be viewed as complementary skills:

    Wireless
        ↓
    Mobile
        ↓
    Cloud
        ↓
    LLM
        ↓
    Blue Team
        ↓
    DevSecOps

Together they expand the traditional web/network penetration-testing mindset into modern security environments.

---

# Final Takeaways

- Modern penetration testing extends far beyond traditional web applications.
- Wireless environments introduce unique network and authentication attack surfaces.
- Mobile testing requires understanding both the application and its backend.
- Cloud security heavily depends on identity, permissions, and configuration.
- LLM applications introduce AI-specific attack surfaces such as prompt injection and jailbreaking.
- Blue Team knowledge helps understand detection, investigation, and response.
- DevSecOps integrates security directly into software development.
- The underlying pentesting mindset remains consistent:
  
    Recon
      ↓
    Enumerate
      ↓
    Identify Weakness
      ↓
    Exploit
      ↓
    Assess Impact
      ↓
    Report

The goal of Specialized Domains is not to master every technology immediately, but to build the ability to recognise different attack surfaces and adapt the penetration-testing methodology to them.