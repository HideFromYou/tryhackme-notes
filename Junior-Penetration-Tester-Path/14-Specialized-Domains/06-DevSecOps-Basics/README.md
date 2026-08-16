# 06 - DevSecOps Basics

## Overview

This room introduces the evolution of software development practices and explains how DevOps evolved into DevSecOps.

The central idea is that security should not be treated as a separate activity performed at the end of development.

Instead, security becomes part of the development culture and is integrated throughout the development process.

    Development
        ↓
    Operations
        ↓
    Automation
        ↓
    Security Integration
        ↓
    DevSecOps

The room covers the evolution of development models, DevOps practices, Shift Left, DevSecOps challenges, DevSecOps culture, and a practical exercise comparing Waterfall, Agile, and DevOps.

---

## Learning Objectives

By completing this room, you should understand:

- How software development practices evolved.
- The differences between Waterfall, Agile, and DevOps.
- The purpose of CI/CD.
- The role of Infrastructure as Code.
- Configuration management and orchestration.
- Why security should shift left.
- What DevSecOps means.
- Common DevSecOps challenges.
- How to build a healthy DevSecOps culture.
- The importance of autonomy, visibility, transparency, understanding, and empathy.

---

# Room Structure

| Lesson | Topic |
|---|---|
| 01 | Introduction |
| 02 | DevOps: A New Era |
| 03 | The Infinite Loop |
| 04 | Shifting Left |
| 05 | DevSecOps: Security Shifts Left |
| 06 | DevSecOps Culture |
| 07 | Exercise: Fuel Trouble |

---

# 01 - Introduction

The room introduces the history and evolution of software development practices and explains why DevSecOps has become important.

The DevSecOps learning path introduced in the room covers:

    Secure SDLC
    Environments
    Tools
    Pipeline Automation
    Source Code Security
    Automated Code Testing
    Dependency Management
    CI/CD
    Environment Security
    Pipeline Security
    Infrastructure as Code
    Cloud DevOps
    Secret Management
    Terraform
    Vagrant
    Docker

The main objective is to understand security as both a discipline and a culture.

---

# 02 - DevOps: A New Era

Software development evolved through several models.

## Waterfall

Waterfall follows a sequential development process.

    Development
        ↓
    Testing
        ↓
    Operations
        ↓
    Delivery

This separation can create:

    Communication Gaps
    Blame
    Backlogs
    Delays
    Unresolved Issues

---

## Agile

Agile introduced greater flexibility and collaboration.

Its core values include:

    Individuals and interactions
        over
    Processes and tools

    Working software
        over
    Comprehensive documentation

    Customer collaboration
        over
    Contract negotiation

    Responding to change
        over
    Following a plan

Agile allows teams to adapt more easily to changing requirements.

---

## DevOps

DevOps focuses on collaboration, integration, automation, and cultural change.

Instead of isolated teams:

    Developers
        ↕
    QA
        ↕
    Operations

DevOps encourages teams to work together.

Important concepts include:

    CI/CD
    Automation
    Infrastructure as Code
    Monitoring
    Collaboration
    Shared Responsibility

---

# 03 - The Infinite Loop

DevOps can be represented as a continuous loop.

Important concepts include:

### CI/CD

Continuous Integration and Continuous Deployment allow frequent changes to be:

    Developed
        ↓
    Integrated
        ↓
    Tested
        ↓
    Deployed

### Infrastructure as Code

Infrastructure is managed through code instead of being configured manually.

Examples include:

    Terraform
    Vagrant

### Configuration Management

Maintains infrastructure in a consistent desired state.

### Orchestration

Automates and coordinates workflows and processes.

### Monitoring

Provides visibility into:

    Performance
    Stability
    Availability
    Problems

### Microservices

Applications can be divided into smaller independent services, improving flexibility and scalability.

---

# 04 - Shifting Left

Shift Left means introducing security earlier in the development lifecycle.

Traditional approach:

    Development
        ↓
    Testing
        ↓
    Production
        ↓
    Security Review

Shift-Left approach:

    Development
        ↓
    Security Testing
        ↓
    Development
        ↓
    Testing
        ↓
    Deployment

The goal is to identify vulnerabilities earlier.

---

## Benefits

Finding vulnerabilities earlier can:

    Reduce Remediation Cost
    Reduce Risk
    Reduce Rollbacks
    Improve Software Quality
    Increase Test Coverage
    Reduce Security Bottlenecks

Security therefore becomes part of development rather than a final checkpoint.

---

# 05 - DevSecOps: Security Shifts Left

DevSecOps integrates security into DevOps as a shared responsibility.

It relies heavily on:

    Automation
    Platform Design
    Collaboration
    Shared Responsibility
    Security Culture

---

## DevSecOps Challenges

### Security Silos

Security can become isolated from development and operations.

This creates:

    Limited Collaboration
    Limited Security Knowledge
    Security Introduced Too Late
    Security Becoming a Blocker

---

### Lack of Visibility & Prioritisation

Teams need visibility into the security state of the services they own.

Without visibility:

    Findings
        ↓
    Backlog
        ↓
    Noise
        ↓
    Poor Prioritisation

---

### Stringent Processes

Overly complicated security processes can slow development.

Security processes should be flexible and should apply stronger controls to higher-risk changes.

---

## Sandboxes

Sandboxes provide isolated environments for experimentation.

The room describes them as environments with:

    No Internal Network Connection
    No Customer Data

This allows developers to experiment without exposing production resources.

---

# 06 - DevSecOps Culture

DevSecOps is not only about security tools.

A successful culture requires:

    Autonomy
    Visibility
    Transparency
    Understanding
    Empathy
    Trust

---

## Promote Autonomy

Teams should be able to make secure decisions independently.

This can be supported through:

    Automation
    Education
    Playbooks
    Runbooks
    Integrated Security Tests

---

## Visibility and Transparency

Teams need visibility into the security state of the services they own.

Security dashboards can help show:

    Findings
    Severity
    Security State
    Priorities

Security tools should also provide developers with useful information such as:

    Affected Code
    Finding Description
    Risk
    Remediation Guidance

This promotes education and autonomy.

---

## Understanding and Empathy

Different teams may have different priorities and definitions of risk.

Effective DevSecOps processes should account for:

    Team Priorities
    Deadlines
    Available Resources
    Service Importance
    Actual Risk

There is no single process that works perfectly for every team.

Understanding how teams work helps security create processes that are practical and sustainable.

---

# 07 - Exercise: Fuel Trouble

The practical exercise compares three software development models:

    Waterfall
    Agile
    DevOps

The scenario involves a space mission where the teams must choose a planet while managing risk and available fuel.

## Results

    Comic 1 → Waterfall
    Comic 2 → Agile
    Comic 3 → DevOps

The exercise demonstrates:

### Waterfall

    Initial Plan
        ↓
    Execute
        ↓
    Test

### Agile

    Plan
        ↓
    Test
        ↓
    Learn
        ↓
    Adapt

### DevOps

    Development
        ↕
    Testing
        ↕
    Operations
        ↕
    Continuous Feedback

---

# DevSecOps Mental Model

The evolution can be summarised as:

    Waterfall
        ↓
    Agile
        ↓
    DevOps
        ↓
    Shift Left
        ↓
    DevSecOps

Security becomes integrated into the development lifecycle rather than remaining an isolated final-stage activity.

---

# Key Takeaways

- Waterfall follows a sequential development model.
- Agile introduces flexibility and responsiveness to change.
- DevOps combines development and operations through collaboration and automation.
- CI/CD enables frequent integration, testing, and deployment.
- Infrastructure as Code allows infrastructure to be managed through code.
- Shift Left moves security earlier in the development lifecycle.
- DevSecOps makes security a shared responsibility.
- Security Silos, Lack of Visibility, and Stringent Processes are important DevSecOps challenges.
- Autonomy, Visibility, Transparency, Understanding, and Empathy are important parts of DevSecOps culture.
- DevSecOps is ultimately about integrating security into the way teams build and operate software.