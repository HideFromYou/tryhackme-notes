# Introduction

## Overview

Modern web applications are built from far more than custom application code. They rely on cloud infrastructure, third-party libraries, cryptographic mechanisms, deployment pipelines, APIs, containers, and increasingly **AI-powered components**. As a result, many of today's most critical security vulnerabilities originate from **design decisions**, **configuration mistakes**, and **operational weaknesses** rather than programming errors.

This room introduces four **OWASP Top 10:2025** categories that focus on application design flaws:

- **AS02 – Security Misconfigurations**
- **AS03 – Software Supply Chain Failures**
- **AS04 – Cryptographic Failures**
- **AS06 – Insecure Design**

Rather than exploiting coding bugs, these vulnerabilities arise when systems are deployed, maintained, or architected insecurely. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1} :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what application design flaws are
- Explain why secure design extends beyond application code
- Recognize the OWASP categories covered in this room
- Understand how poor architectural decisions introduce security risks
- Prepare for the practical examples in later lessons

---

## Main Content

### Security Starts Before Coding

Many security issues originate long before software is deployed.

Examples include:

- Unsafe default configurations
- Weak architectural decisions
- Poor dependency management
- Incorrect cryptographic implementation
- Missing threat modelling

These weaknesses become part of the application's foundation and may affect every component built on top of it.

---

### Beyond Programming Bugs

Not every vulnerability results from insecure code.

Applications may become vulnerable because of:

- Deployment mistakes
- Misconfigured services
- Untrusted dependencies
- Weak security assumptions
- Poor operational practices

These issues often remain unnoticed until exploited by attackers.

---

### OWASP Top 10 Focus

This room examines four OWASP Top 10:2025 categories:

- **AS02 – Security Misconfigurations**
- **AS03 – Software Supply Chain Failures**
- **AS04 – Cryptographic Failures**
- **AS06 – Insecure Design**

Together, these categories emphasize building security into every stage of development, deployment, and maintenance. :contentReference[oaicite:4]{index=4} :contentReference[oaicite:5]{index=5} :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

---

### Secure-by-Design

The room promotes a **secure-by-design** approach, where security requirements are considered from the beginning rather than added after deployment.

This includes:

- Designing secure architectures
- Reviewing configurations
- Verifying dependencies
- Applying strong cryptography
- Performing continuous threat modelling

Security is most effective when integrated throughout the Software Development Life Cycle (SDLC).

---

## Skills Practiced

- Secure Application Design
- Threat Modeling
- Secure SDLC
- Security Architecture
- OWASP Top 10

---

## Key Takeaways

- Application security depends on architecture, deployment, and operational practices as much as application code.
- Many critical vulnerabilities originate from insecure design decisions.
- This room focuses on Security Misconfigurations, Software Supply Chain Failures, Cryptographic Failures, and Insecure Design.
- Secure systems require security to be considered throughout the entire development lifecycle.
- Designing securely from the beginning significantly reduces future security risks. :contentReference[oaicite:8]{index=8} :contentReference[oaicite:9]{index=9} :contentReference[oaicite:10]{index=10} :contentReference[oaicite:11]{index=11}