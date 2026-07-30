# XSS Introduction

## Overview

Cross-Site Scripting (XSS) is one of the most common and impactful vulnerabilities found in modern web applications. It occurs when an application allows untrusted input to be interpreted as executable code by a user's browser. Successful XSS attacks can compromise user sessions, manipulate web pages, steal sensitive information, and perform actions on behalf of victims.

This room introduces the core concepts behind XSS, explores the different types of XSS vulnerabilities, and explains how attackers exploit insecure input handling. It also highlights the importance of proper validation, output encoding, and secure development practices for preventing client-side attacks.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand what Cross-Site Scripting (XSS) is
- Explain how browsers execute client-side JavaScript
- Differentiate between the major types of XSS vulnerabilities
- Recognise common attack scenarios and their potential impact
- Understand defensive techniques used to mitigate XSS

---

## Lessons

### 1. Introduction

Introduces the fundamentals of XSS and explains why client-side code execution represents a significant security risk in web applications.

### 2. Important Terminologies

Covers essential concepts such as JavaScript, the Document Object Model (DOM), cookies, sessions, and URL parameters that form the foundation for understanding XSS.

### 3. XSS Payload

Explains what XSS payloads are, how browsers interpret injected JavaScript, and why understanding payload behaviour is important during security testing.

### 4. Reflected XSS (Non-Persistent)

Introduces reflected XSS, where malicious input is immediately returned by the application and executed within the victim's browser.

### 5. Stored XSS (Persistent)

Explores persistent XSS vulnerabilities in which malicious content is stored by the application and later delivered to multiple users.

### 6. DOM-Based XSS (Client-Side)

Examines client-side XSS vulnerabilities that occur when JavaScript manipulates untrusted data directly within the browser's Document Object Model.

### 7. Blind XSS

Introduces blind XSS, where injected scripts execute later in a different user's browser, often within administrative interfaces or internal systems.

### 8. Perfecting Your Payload

Discusses how payload construction influences reliability and demonstrates the importance of understanding browser behaviour during security assessments.

### 9. Summary

Reviews the key concepts covered throughout the room and reinforces the techniques used to identify and understand XSS vulnerabilities.

---

## Skills Practiced

- Cross-Site Scripting (XSS) Fundamentals
- Client-Side Security
- JavaScript Security Concepts
- HTTP Request Analysis
- Web Application Security Assessment
- Secure Input Handling
- Vulnerability Identification

---

## Tools Used

- Web Browser
- Browser Developer Tools
- JavaScript
- HTML
- TryHackMe AttackBox

---

## Key Takeaways

- XSS vulnerabilities occur when applications improperly handle untrusted input.
- Different XSS variants exploit different stages of how applications process user-controlled data.
- Understanding browser behaviour is essential when analysing client-side vulnerabilities.
- Proper input validation, output encoding, and secure coding practices significantly reduce XSS risk.
- XSS remains one of the most important vulnerabilities to understand for both penetration testers and secure software developers.