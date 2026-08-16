# 04 - Shifting Left

## Overview

"Shifting Left" means introducing security earlier in the software development lifecycle.

Instead of performing security testing only at the end:

    Development
        ↓
    Testing
        ↓
    Production
        ↓
    Security Review

Security becomes:

    Development
        ↓
    Security
        ↓
    Testing
        ↓
    Deployment
        ↓
    Production

---

## Traditional Security Model

Historically, security testing was often performed near the end of the development lifecycle.

The result could be:

    Security Testing
        ↓
    Vulnerability Found
        ↓
    Development Blocked
        ↓
    Fix Required
        ↓
    Delay / Rollback

This created:

    Delays
    Friction
    Higher Remediation Costs
    Rollbacks

---

## Shift-Left Approach

Security controls are introduced throughout development.

Examples include:

    Code Analysis
    Automated Tests
    Security Testing
    Infrastructure Analysis

Security flaws can therefore be identified while development is still taking place.

---

## Why Shift Left?

Modern DevOps environments are much faster.

Cloud infrastructure can be provisioned automatically and software can be released frequently.

This increased speed can also introduce security risks.

If security only happens after development:

    Fast Development
        ↓
    Security Review
        ↓
    Large Backlog
        ↓
    Bottleneck

Shift Left attempts to prevent this bottleneck.

---

## Benefits

Finding vulnerabilities earlier can:

    Reduce Remediation Cost
    Reduce Rollbacks
    Reduce Risk
    Improve Software Quality
    Improve Trust
    Increase Development Speed

---

## DevSecOps

The development approach of integrating security throughout DevOps is referred to as:

    DevSecOps

Security becomes part of the development process instead of being treated as an add-on.

---

## Core Principle

Security is not:

    "Something we check at the end."

Security is:

    "Something we build into the development process."

---

## Key Takeaways

- Shift Left means moving security towards the earliest stages of development.
- Traditional late-stage security testing can create bottlenecks.
- Automated security testing helps identify flaws earlier.
- Earlier detection reduces remediation cost and risk.
- DevSecOps applies the Shift-Left approach to DevOps.