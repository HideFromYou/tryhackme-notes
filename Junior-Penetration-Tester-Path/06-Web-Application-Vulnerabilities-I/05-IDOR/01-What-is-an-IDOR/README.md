# What is an IDOR?

## Overview

Insecure Direct Object Reference (IDOR) is an access control vulnerability that occurs when a web application exposes a direct reference to an internal object without verifying whether the authenticated user is authorised to access it. Instead of validating ownership or permissions, the application trusts the user-supplied identifier, potentially allowing access to resources belonging to other users.

This lesson introduces the fundamentals of IDOR, explains its relationship to Broken Access Control, and highlights why proper authorisation is essential for protecting sensitive resources.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Define an Insecure Direct Object Reference (IDOR)
- Understand the difference between authentication and authorisation
- Explain why IDOR is classified as an access control vulnerability
- Recognise the potential impact of missing authorisation checks
- Understand the importance of server-side access validation

---

## Main Content

### What is an IDOR?

An IDOR vulnerability occurs when an application uses a user-supplied object identifier to retrieve a resource without verifying that the requester has permission to access it.

Examples of protected objects include:

- User profiles
- Orders
- Documents
- Support tickets
- Images
- Financial records

Every request for these resources should include a server-side authorisation check.

---

### Authentication vs Authorisation

Authentication answers the question:

> **Who is the user?**

Authorisation answers the question:

> **Is this user allowed to access this specific resource?**

An application may correctly authenticate a user while still failing to verify whether they are authorised to access another user's data.

---

### Why IDOR Matters

IDOR is considered one of the most important web application vulnerabilities because exploitation is often straightforward while the impact can be severe.

Potential consequences include:

- Exposure of sensitive information
- Modification of another user's data
- Deletion of protected resources
- Unauthorised account actions
- Privilege escalation in poorly designed applications

---

### Secure Access Control

Applications should never rely on object identifiers alone to determine access.

Every request should verify:

- The user's identity
- Ownership of the requested resource
- Appropriate permissions
- Applicable access control rules

Proper server-side authorisation is the primary defence against IDOR vulnerabilities.

---

## Skills Practiced

- IDOR Fundamentals
- Broken Access Control
- Authorisation Concepts
- Web Application Security
- Secure Access Control

---

## Key Takeaways

- IDOR is caused by missing or insufficient server-side authorisation checks.
- Authentication does not guarantee authorisation.
- Every object reference should be validated against the current user's permissions.
- Strong access control is essential for protecting sensitive application resources.