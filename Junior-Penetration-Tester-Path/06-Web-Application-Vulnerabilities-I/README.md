# Web Application Vulnerabilities

## Overview

This section focuses on understanding some of the most common vulnerabilities affecting modern web applications. Through a combination of theoretical lessons and practical exercises, these rooms explore how insecure application design can lead to serious security issues and how proper defensive practices help prevent them.

The content covers authentication and authorisation flaws, injection attacks, client-side vulnerabilities, server-side request handling, and broken access control. By completing these rooms, learners gain a solid foundation in identifying common web security weaknesses and understanding how secure applications should be designed.

---

## Learning Objectives

After completing this section, you should be able to:

- Understand the fundamentals of common web application vulnerabilities
- Explain how SQL Injection attacks occur and how they are mitigated
- Describe Cross-Site Request Forgery (CSRF) attacks and available defenses
- Differentiate between the major types of Cross-Site Scripting (XSS)
- Understand Server-Side Request Forgery (SSRF) concepts and associated risks
- Explain how Insecure Direct Object References (IDOR) result from broken access control
- Recognise insecure authentication and authorisation mechanisms
- Understand secure design principles used to protect modern web applications

---

## Rooms Included

### 1. SQL Injection Introduction

Introduces SQL Injection fundamentals, including how applications interact with databases, the different categories of SQL Injection, and defensive techniques used to prevent injection vulnerabilities.

### 2. CSRF Introduction

Explores Cross-Site Request Forgery, explaining how attackers abuse authenticated user sessions and how modern web applications defend against these attacks.

### 3. XSS Introduction

Covers the fundamentals of Cross-Site Scripting, including Reflected, Stored, DOM-Based, and Blind XSS, together with common prevention strategies.

### 4. Intro to SSRF

Introduces Server-Side Request Forgery, explains how server-side requests can be abused, discusses common SSRF defenses, and demonstrates secure application design principles.

### 5. IDOR

Focuses on Broken Access Control through Insecure Direct Object References, covering direct object references, encoded and hashed identifiers, unpredictable IDs, and secure server-side authorisation.

### 6. Recruit

A practical challenge room that combines multiple web application security concepts into a realistic assessment, encouraging systematic enumeration, authentication analysis, authorisation testing, and secure application evaluation.

---

## Skills Developed

Throughout this section, you will practice:

- Web Application Security
- SQL Injection Fundamentals
- Cross-Site Request Forgery (CSRF)
- Cross-Site Scripting (XSS)
- Server-Side Request Forgery (SSRF)
- Broken Access Control
- IDOR Analysis
- Authentication Testing
- Authorisation Assessment
- HTTP Request Analysis
- Web Enumeration
- Secure Application Design

---

## Tools Used

- Web Browser
- Burp Suite
- Browser Developer Tools
- HTTP Proxy
- SQL Clients (Conceptually)
- Web Security Testing Utilities

---

## Key Takeaways

- Web application security relies heavily on secure server-side validation.
- Authentication and authorisation serve different purposes and must both be implemented correctly.
- User-supplied input should never be trusted without validation.
- Access control should be enforced consistently across every endpoint and resource.
- Modern web applications require layered security controls to defend against a wide range of attack techniques.
- Understanding common vulnerabilities is essential for both penetration testing and secure software development.