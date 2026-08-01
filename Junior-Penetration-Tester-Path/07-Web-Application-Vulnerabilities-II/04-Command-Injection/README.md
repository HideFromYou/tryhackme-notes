# Command Injection

## Overview

Command Injection is a critical web application vulnerability that occurs when an application executes operating system commands using untrusted user input. If user-supplied data is passed directly to shell commands without proper validation or sanitisation, attackers may execute arbitrary commands, access sensitive information, or completely compromise the underlying server.

This room introduces the fundamentals of Command Injection, explains the differences between Blind and Verbose Command Injection, demonstrates practical exploitation techniques, and explores secure coding practices used to prevent command execution vulnerabilities. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this room, you should be able to:

- Understand what Command Injection is
- Explain how operating system command execution vulnerabilities occur
- Differentiate between Blind and Verbose Command Injection
- Recognise common command injection payloads
- Understand secure mitigation techniques
- Apply command injection concepts during practical assessments

---

## Lessons

### 1. Introduction

Introduces Command Injection, explains how web applications interact with operating system commands, and demonstrates how insecure input handling creates command execution vulnerabilities.

### 2. Blind & Verbose Command Injection

Explores the two primary forms of Command Injection, demonstrates detection techniques, and introduces common Linux and Windows payloads used during assessments. :contentReference[oaicite:1]{index=1}

### 3. Remediation – Sanitisation

Examines defensive coding techniques, proper input validation, sanitisation, and secure methods for executing system commands.

### 4. Practical Command Injection

Provides a hands-on laboratory where learners identify and exploit Command Injection vulnerabilities within intentionally vulnerable applications.

---

## Skills Practiced

- Command Injection
- Blind Command Injection
- Verbose Command Injection
- Operating System Commands
- Input Validation
- Input Sanitisation
- Web Application Security
- Vulnerability Assessment

---

## Tools Used

- Web Browser
- Burp Suite
- Browser Developer Tools
- Linux Terminal
- Windows Command Prompt
- TryHackMe AttackBox

---

## Key Takeaways

- Command Injection occurs when applications execute operating system commands using untrusted user input.
- Blind and Verbose Command Injection require different testing methodologies.
- Operating system commands should never be built directly from user-controlled input.
- Proper input validation, sanitisation, parameterisation, and least-privilege execution significantly reduce Command Injection risk.
- Secure coding practices remain the most effective defence against operating system command execution vulnerabilities. :contentReference[oaicite:2]{index=2}