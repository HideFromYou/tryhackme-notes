# What is IAAA?

## Overview

**IAAA** is a simple model that describes how applications securely identify users, verify their identity, determine what they are allowed to do, and record their actions. The four components—**Identity, Authentication, Authorisation, and Accountability**—must work together in sequence. Each stage depends on the previous one, meaning later stages cannot function correctly if an earlier stage has failed.

The three OWASP Top 10:2025 categories covered in this room are all examples of failures in the implementation of IAAA. Weaknesses in any of these areas can allow attackers to access other users' data or obtain privileges they should not have. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Define IAAA
- Explain each component of the IAAA model
- Understand the relationship between the four stages
- Recognize why each stage depends on the previous one
- Relate IAAA failures to OWASP Top 10 vulnerabilities

---

## Main Content

### Identity

**Identity** is the unique account that represents a user or service.

Examples include:

- Username
- Email address
- User ID
- Service account

Identity answers the question:

> **Who is the user?** :contentReference[oaicite:1]{index=1}

---

### Authentication

**Authentication** verifies that a user is actually the identity they claim to be.

Common authentication methods include:

- Passwords
- One-Time Passwords (OTP)
- Passkeys
- Multi-Factor Authentication (MFA)

Authentication answers the question:

> **Can the user prove their identity?** :contentReference[oaicite:2]{index=2}

---

### Authorisation

**Authorisation** determines what an authenticated user is allowed to access or perform.

Examples include:

- Viewing personal data
- Editing resources
- Accessing administrative functions
- Performing privileged operations

Authorisation answers the question:

> **What is the user allowed to do?** :contentReference[oaicite:3]{index=3}

---

### Accountability

**Accountability** ensures that user actions are recorded and monitored.

Typical accountability mechanisms include:

- Audit logs
- Authentication logs
- Security alerts
- Activity monitoring

Accountability answers the question:

> **Who performed which action, when, and from where?** :contentReference[oaicite:4]{index=4}

---

### Why Order Matters

The four components must occur in sequence:

1. Identity
2. Authentication
3. Authorisation
4. Accountability

It is not possible to safely perform a later stage if an earlier one has failed.

For example:

- Without a valid identity, authentication cannot occur.
- Without successful authentication, authorisation decisions cannot be trusted.
- Without accountability, security events cannot be investigated. :contentReference[oaicite:5]{index=5}

---

## Skills Practiced

- Identity Management
- Authentication Security
- Access Control
- Security Monitoring
- Web Application Security

---

## Key Takeaways

- IAAA stands for **Identity, Authentication, Authorisation, and Accountability**.
- Each component serves a distinct purpose within the application security lifecycle.
- The four stages must be performed in order because each depends on the previous one.
- Weak implementations of IAAA contribute directly to multiple OWASP Top 10 vulnerabilities.
- Strong identity management requires secure implementation across all four components. :contentReference[oaicite:6]{index=6}