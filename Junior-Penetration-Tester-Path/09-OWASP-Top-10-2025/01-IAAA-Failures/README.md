# IAAA Failures

## Overview

This room introduces the **Identity, Authentication, Authorisation, and Accountability (IAAA)** model and explains how weaknesses in its implementation lead to several categories within the **OWASP Top 10:2025**. Rather than focusing on a single vulnerability, the room demonstrates how failures across the identity lifecycle can allow attackers to access unauthorized data, impersonate other users, escalate privileges, or perform malicious actions without being detected.

Through practical examples, you will explore three OWASP Top 10 categories:

- **A01 – Broken Access Control**
- **A07 – Authentication Failures**
- **A09 – Logging & Alerting Failures**

Each lesson highlights common implementation mistakes and demonstrates why strong IAAA controls are fundamental to secure web applications. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1} :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

---

## Learning Objectives

After completing this room, you should be able to:

- Understand the IAAA model
- Differentiate between Identity, Authentication, Authorisation, and Accountability
- Identify Broken Access Control vulnerabilities
- Recognize common Authentication Failures
- Explain the importance of application logging and alerting
- Apply secure design principles to web applications

---

## Lessons

### 1. Introduction

Introduces the OWASP Top 10:2025 categories covered in the room and explains why secure implementation of IAAA is essential for protecting web applications.

---

### 2. What is IAAA?

Explains the four components of the IAAA model:

- Identity
- Authentication
- Authorisation
- Accountability

and how weaknesses in these areas contribute to OWASP Top 10 vulnerabilities. :contentReference[oaicite:4]{index=4}

---

### 3. A01 – Broken Access Control

Demonstrates how insufficient server-side authorization checks can lead to **Insecure Direct Object References (IDOR)**, horizontal privilege escalation, and unauthorized access to another user's data. :contentReference[oaicite:5]{index=5}

---

### 4. A07 – Authentication Failures

Explores common authentication weaknesses including username enumeration, weak authentication logic, insecure session handling, and account confusion vulnerabilities that may allow attackers to access other users' accounts. :contentReference[oaicite:6]{index=6}

---

### 5. A09 – Logging & Alerting Failures

Explains why logging, monitoring, and alerting are essential for detecting attacks, investigating incidents, and maintaining accountability within an application. :contentReference[oaicite:7]{index=7}

---

### 6. Conclusion

Summarizes the security principles covered throughout the room and reinforces best practices for implementing secure Identity, Authentication, Authorisation, and Accountability controls. :contentReference[oaicite:8]{index=8}

---

## Skills Practiced

- Identity Management
- Authentication Security
- Access Control
- Privilege Escalation Analysis
- Web Application Security
- Logging & Monitoring
- Secure Application Design
- OWASP Top 10

---

## Tools & Technologies

- Web Applications
- HTTP
- Browser Developer Tools
- Server-side Authorization
- Authentication Systems
- Application Logs

---

## Key Takeaways

- IAAA provides a framework for implementing secure identity and access management.
- Broken Access Control remains one of the most critical web application vulnerabilities.
- Authentication mechanisms must securely verify user identities and manage sessions.
- Logging and alerting are essential for detecting attacks and supporting incident response.
- Secure applications require strong controls across every stage of the IAAA lifecycle, not just authentication alone. :contentReference[oaicite:9]{index=9} :contentReference[oaicite:10]{index=10} :contentReference[oaicite:11]{index=11} :contentReference[oaicite:12]{index=12} :contentReference[oaicite:13]{index=13}