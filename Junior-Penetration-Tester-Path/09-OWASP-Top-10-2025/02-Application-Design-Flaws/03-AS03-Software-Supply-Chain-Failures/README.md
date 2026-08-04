# AS03 - Software Supply Chain Failures

## Overview

**Software Supply Chain Failures** occur when applications depend on third-party components, libraries, services, software updates, build pipelines, or AI models that are compromised, outdated, or insufficiently verified. Rather than attacking an organization's own code, attackers target the software and tools it trusts, allowing malicious code or functionality to spread throughout the entire application.

Modern software is built on numerous external dependencies, making supply chain security a critical part of application security. A single compromised dependency can affect thousands of systems that rely on it. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Software Supply Chain Failures are
- Explain why third-party dependencies introduce security risks
- Recognize common supply chain attack patterns
- Understand the importance of securing build pipelines
- Apply supply chain security best practices

---

## Main Content

### What are Software Supply Chain Failures?

Software Supply Chain Failures occur when applications rely on external software components that are compromised, vulnerable, or improperly verified.

These components may include:

- Libraries
- Frameworks
- APIs
- Software updates
- Build pipelines
- AI models

Although the vulnerability does not exist within the application's own code, attackers can exploit trusted dependencies to compromise the system. :contentReference[oaicite:1]{index=1}

---

### Why They Matter

Modern applications rarely operate independently.

Instead, they rely on numerous third-party components that may introduce security risks if they are:

- Outdated
- Unmaintained
- Malicious
- Improperly verified

A single compromised dependency may allow attackers to bypass traditional security controls and compromise the entire application. :contentReference[oaicite:2]{index=2}

---

### Common Supply Chain Weaknesses

The room identifies several common weaknesses:

- Using unverified or unmaintained libraries
- Automatically installing updates without verification
- Blind trust in third-party AI models
- Insecure CI/CD build pipelines
- Poor dependency provenance tracking
- Failure to monitor dependencies after deployment :contentReference[oaicite:3]{index=3}

---

### Real-World Example

The room highlights the **SolarWinds Orion** compromise, where attackers inserted malicious code into a trusted software update.

Organizations that installed the compromised update unknowingly introduced the attacker into their own environments.

This incident demonstrates how compromising the software supply chain can affect thousands of downstream systems simultaneously. :contentReference[oaicite:4]{index=4}

---

### Protecting the Supply Chain

Recommended defensive practices include:

- Verify third-party libraries and AI models before use.
- Monitor dependencies for newly discovered vulnerabilities.
- Sign and verify software updates.
- Secure CI/CD pipelines against tampering.
- Track dependency provenance and licensing.
- Monitor runtime behavior for unusual activity.
- Integrate supply chain threat modeling throughout the SDLC. :contentReference[oaicite:5]{index=5}

---

## Skills Practiced

- Supply Chain Security
- Dependency Management
- CI/CD Security
- Software Integrity
- Secure SDLC
- Threat Modeling

---

## Key Takeaways

- Software Supply Chain Failures originate from trusted third-party components rather than an application's own code.
- Libraries, software updates, build pipelines, APIs, and AI models all form part of the software supply chain.
- Blind trust in external dependencies significantly increases organizational risk.
- Continuous verification, monitoring, and secure build processes are essential for defending against supply chain attacks.
- Supply chain security should be integrated into every stage of the Software Development Life Cycle (SDLC). :contentReference[oaicite:6]{index=6}