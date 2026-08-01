# Broken Authentication

## Overview

Broken Authentication refers to security weaknesses that allow attackers to bypass or compromise a web application's authentication mechanisms. These vulnerabilities may enable unauthorised users to gain access to accounts, impersonate legitimate users, or elevate their privileges without possessing valid credentials.

This room explores common authentication bypass techniques, including username enumeration, brute-force attacks, logic flaws, and insecure cookie handling. It also demonstrates defensive practices that strengthen authentication systems and reduce the risk of account compromise.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand what Broken Authentication is
- Identify common authentication bypass techniques
- Recognise username enumeration vulnerabilities
- Understand brute-force attacks against login forms
- Identify authentication logic flaws
- Explain how insecure cookies can lead to authentication bypass
- Understand best practices for securing authentication mechanisms

---

## Lessons

### 1. Introduction

Introduces Broken Authentication, explains why authentication mechanisms are targeted by attackers, and outlines the concepts covered throughout the room.

### 2. Types of Authentication Bypass

Explores common methods attackers use to bypass authentication, including weaknesses in application logic, session handling, and credential validation.

### 3. Username Enumeration

Explains how applications may unintentionally reveal whether a username exists through differences in responses, error messages, or response timing.

### 4. Brute Forcing a Login Form

Introduces brute-force attacks against authentication systems and discusses defensive mechanisms such as rate limiting, account lockout, and multi-factor authentication.

### 5. Logic Flaws

Examines authentication weaknesses caused by insecure application logic rather than technical vulnerabilities, highlighting the importance of secure workflow design.

### 6. Cookie Manipulation

Explores how insecure client-side cookies can be modified to bypass authentication or elevate privileges when proper integrity validation is missing.

### 7. Conclusion

Summarises the key authentication bypass techniques covered throughout the room and reviews defensive strategies for securing authentication systems.

---

## Skills Practiced

- Authentication Security
- Broken Authentication
- Username Enumeration
- Brute-Force Analysis
- Session Security
- Cookie Security
- Authentication Logic Assessment
- Web Application Security

---

## Tools Used

- Web Browser
- Burp Suite
- Browser Developer Tools
- HTTP Requests
- TryHackMe AttackBox

---

## Key Takeaways

- Authentication systems are a primary target for attackers and must be carefully designed.
- Small implementation mistakes can lead to complete authentication bypass.
- Username enumeration often provides valuable information for further attacks.
- Strong authentication combines secure implementation, rate limiting, MFA, and robust session management.
- Secure server-side validation is essential for preventing authentication-related vulnerabilities.