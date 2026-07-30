# Defeating Common SSRF Defenses

## Overview

To reduce the risk of Server-Side Request Forgery (SSRF), developers often implement validation mechanisms that restrict where an application can send outbound requests. While these protections improve security, weak or incomplete implementations may still leave applications vulnerable.

This lesson introduces common SSRF defence mechanisms, explains how they are intended to work, and highlights the importance of implementing them correctly as part of a layered security strategy.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand common SSRF mitigation techniques
- Differentiate between allow lists and deny lists
- Explain why URL validation is challenging
- Recognise implementation weaknesses in SSRF defences
- Understand the importance of defence in depth

---

## Main Content

### Deny Lists

A deny list blocks requests to specific destinations that are considered unsafe.

Examples of restricted targets may include:

- Localhost
- Internal IP addresses
- Loopback interfaces
- Cloud metadata services

Although deny lists provide a basic level of protection, they rely on accurately identifying every prohibited destination, making them difficult to maintain.

---

### Allow Lists

An allow list permits requests only to predefined trusted destinations.

This approach generally provides stronger security because all other destinations are rejected by default.

However, effective protection depends on proper URL parsing and strict validation rather than simple string comparisons.

---

### URL Validation

Applications should carefully validate every component of a user-supplied destination before generating a server-side request.

Validation should consider:

- Hostnames
- IP addresses
- Protocols
- Ports
- URL structure

Incomplete validation may allow unexpected request destinations despite existing security controls.

---

### Layered Security Controls

Effective SSRF protection combines multiple defensive techniques rather than relying on a single mechanism.

Common security controls include:

- Allow lists
- Network segmentation
- Firewall rules
- Secure URL parsing
- Request validation
- Cloud metadata protections

Using several layers of defence significantly improves application resilience.

---

### Secure Application Design

Preventing SSRF begins during application design.

Developers should minimise unnecessary outbound requests, carefully validate user-controlled input, and ensure that internal services are not exposed solely because requests originate from trusted application servers.

Security controls should be consistently applied across all features that generate server-side requests.

---

## Skills Practiced

- SSRF Mitigation
- URL Validation Concepts
- Secure Application Design
- Web Application Security
- Defence in Depth

---

## Key Takeaways

- SSRF protection requires more than simply blocking a small number of destinations.
- Allow lists generally provide stronger protection than deny lists when implemented correctly.
- Proper URL parsing and validation are essential components of secure SSRF prevention.
- Combining multiple defensive mechanisms provides stronger protection against server-side request forgery.
- Secure application design plays a critical role in reducing SSRF risk.