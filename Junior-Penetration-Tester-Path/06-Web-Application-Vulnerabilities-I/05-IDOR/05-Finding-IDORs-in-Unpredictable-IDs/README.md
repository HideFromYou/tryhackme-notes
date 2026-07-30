# Finding IDORs in Unpredictable IDs

## Overview

Some web applications use randomly generated identifiers, Universally Unique Identifiers (UUIDs), or other non-sequential values to make object references difficult to predict. While these identifiers reduce the risk of simple enumeration attacks, they do not prevent Insecure Direct Object Reference (IDOR) vulnerabilities if the application fails to enforce proper authorisation.

This lesson explains why unpredictable identifiers improve obscurity but cannot replace server-side access control.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the purpose of unpredictable object identifiers
- Explain why random identifiers do not eliminate IDOR vulnerabilities
- Recognise how authorisation differs from identifier complexity
- Understand secure methods for validating object ownership
- Appreciate the importance of server-side access control

---

## Main Content

### Unpredictable Identifiers

Modern applications often assign resources identifiers that are difficult to guess.

Examples include:

- UUIDs
- Random strings
- Universally unique tokens
- System-generated object references

These identifiers make sequential enumeration significantly more difficult.

---

### Enumeration vs Authorisation

Using unpredictable identifiers primarily protects against identifier guessing.

However, it does **not** answer the most important security question:

> **Is the authenticated user authorised to access this resource?**

Even if an identifier cannot be guessed, the application must still verify ownership before returning the requested object.

---

### Verifying Access Control

Security testing should focus on whether the server validates permissions rather than how complex an identifier appears.

Authorisation checks should verify:

- User identity
- Resource ownership
- Assigned permissions
- Access control policies

Without these checks, unpredictable identifiers alone cannot prevent IDOR vulnerabilities.

---

### Secure Design Principles

Applications should combine strong identifier design with robust access control.

Recommended practices include:

- Server-side authorisation checks
- Resource ownership validation
- Role-based access control
- Least privilege principles
- Consistent permission enforcement

Proper authorisation remains the foundation of secure object access.

---

## Skills Practiced

- IDOR Analysis
- Access Control Validation
- Secure Authorisation
- Web Application Security
- Resource Ownership Verification

---

## Key Takeaways

- Unpredictable identifiers reduce the risk of simple enumeration but do not provide access control.
- Every request for a protected resource requires server-side authorisation validation.
- Security depends on verifying permissions, not on hiding object identifiers.
- Strong access control combined with well-designed identifiers provides significantly better protection against IDOR vulnerabilities.