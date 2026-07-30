# Intro to SSRF

## Overview

Server-Side Request Forgery (SSRF) is a web application vulnerability that allows an attacker to manipulate a server into making unintended HTTP requests on their behalf. Because these requests originate from the application itself, they often inherit the server's level of trust, potentially exposing internal services, sensitive data, and cloud resources that are not directly accessible from the internet.

This room introduces the fundamentals of SSRF, explains how different types of SSRF vulnerabilities work, demonstrates common attack scenarios, and explores defensive techniques used to secure server-side applications.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand what Server-Side Request Forgery (SSRF) is
- Differentiate between Regular and Blind SSRF
- Recognise common SSRF attack vectors
- Understand the security impact of SSRF vulnerabilities
- Identify common defensive mechanisms and their limitations

---

## Lessons

### 1. Introduction

Introduces the concept of Server-Side Request Forgery, explains why it occurs, and explores the potential impact on internal infrastructure and cloud environments.

### 2. SSRF Examples

Examines several common ways applications construct server-side requests and demonstrates typical locations where SSRF vulnerabilities may appear.

### 3. Finding an SSRF

Focuses on identifying application functionality that may be vulnerable to SSRF and introduces a structured methodology for recognising potential attack surfaces.

### 4. Defeating Common SSRF Defenses

Explores common mitigation techniques, including allow lists, deny lists, and URL validation, while discussing implementation weaknesses that can reduce their effectiveness.

### 5. SSRF Practical

Applies the concepts learned throughout the room in a practical lab designed to reinforce SSRF identification and analysis skills.

---

## Skills Practiced

- Server-Side Request Forgery (SSRF)
- HTTP Request Analysis
- URL Validation Concepts
- Web Application Security
- Internal Network Security
- Cloud Security Fundamentals
- Vulnerability Assessment

---

## Tools Used

- Web Browser
- Browser Developer Tools
- Burp Suite
- TryHackMe AttackBox

---

## Key Takeaways

- SSRF allows attackers to influence server-side requests made by an application.
- Requests originating from trusted servers may access resources unavailable to external users.
- SSRF vulnerabilities can expose internal services, cloud metadata, and sensitive infrastructure.
- Secure URL validation and properly designed access controls are essential for reducing SSRF risk.
- Understanding both attack techniques and defensive strategies is fundamental to securing modern web applications.