# IDOR

## Overview

Insecure Direct Object Reference (IDOR) is a common access control vulnerability that occurs when a web application exposes direct references to internal objects without verifying whether the authenticated user is authorised to access them. Although the user is successfully authenticated, the application fails to enforce proper authorisation, allowing access to resources belonging to other users.

This room introduces the fundamentals of IDOR, explains how different types of object identifiers are used by applications, explores common locations where IDOR vulnerabilities appear, and demonstrates how proper access control prevents unauthorised access.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand what an Insecure Direct Object Reference (IDOR) vulnerability is
- Explain the difference between authentication and authorisation
- Identify different forms of object identifiers
- Recognise common locations where IDOR vulnerabilities appear
- Understand secure access control principles used to prevent IDOR

---

## Lessons

### 1. What is an IDOR?

Introduces the concept of IDOR, explains its relationship to Broken Access Control, and discusses why missing authorisation checks create security risks.

### 2. An IDOR Example

Demonstrates how modifying object identifiers can expose resources belonging to other users when proper server-side authorisation is absent.

### 3. Finding IDORs in Encoded IDs

Explores how encoded identifiers may provide a false sense of security and explains why encoding alone does not prevent IDOR vulnerabilities.

### 4. Finding IDORs in Hashed IDs

Examines hashed object identifiers and discusses why hashing predictable values should never replace proper authorisation checks.

### 5. Finding IDORs in Unpredictable IDs

Introduces randomly generated identifiers and explains why unpredictable values reduce enumeration but do not eliminate IDOR vulnerabilities.

### 6. Where are IDORs Located?

Reviews the many locations where object references may appear, including URLs, APIs, request bodies, cookies, headers, and background requests.

### 7. A Practical IDOR Example

Applies the concepts covered throughout the room in a practical exercise focused on identifying and analysing insecure object references.

---

## Skills Practiced

- Insecure Direct Object Reference (IDOR)
- Broken Access Control
- Object-Level Authorisation
- HTTP Request Analysis
- Web Application Security
- API Security Fundamentals
- Vulnerability Assessment

---

## Tools Used

- Web Browser
- Browser Developer Tools
- Burp Suite
- TryHackMe AttackBox

---

## Key Takeaways

- IDOR is an access control vulnerability caused by missing server-side authorisation checks.
- Authentication alone does not guarantee that a user is authorised to access every resource.
- Object identifiers may appear in many formats, but none provide security without proper access control.
- Every server-side request that references an object should validate user permissions.
- Strong authorisation logic is essential for protecting sensitive application resources.