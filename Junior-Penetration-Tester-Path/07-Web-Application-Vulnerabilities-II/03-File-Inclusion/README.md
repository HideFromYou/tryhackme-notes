# File Inclusion

## Overview

File Inclusion vulnerabilities occur when a web application allows user-controlled input to determine which files are loaded or processed by the server. Depending on the implementation, these vulnerabilities may allow attackers to read sensitive files, execute server-side code, or even achieve remote code execution.

This room introduces the different types of file inclusion vulnerabilities, including Path Traversal, Local File Inclusion (LFI), and Remote File Inclusion (RFI). Through practical exercises, it demonstrates how these vulnerabilities arise, how they can be exploited in controlled environments, and how developers can prevent them using secure coding practices. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this room, you should be able to:

- Understand the differences between Path Traversal, LFI, and RFI
- Identify file inclusion entry points in web applications
- Explain how Local and Remote File Inclusion vulnerabilities occur
- Recognise the security risks associated with insecure file handling
- Apply secure coding practices to mitigate file inclusion vulnerabilities

---

## Lessons

### 1. Introduction

Introduces file inclusion vulnerabilities, explains their relationship to the OWASP Top 10, and outlines the concepts covered throughout the room.

### 2. Deploy the VM

Sets up the practical laboratory environment used throughout the room to demonstrate file inclusion vulnerabilities safely.

### 3. Path Traversal

Explores directory traversal attacks and demonstrates how attackers attempt to access files outside the intended application directory.

### 4. Local File Inclusion (LFI)

Introduces Local File Inclusion, explaining how unsafe server-side file inclusion functions can expose sensitive files or execute unintended code.

### 5. Local File Inclusion (LFI) Continued

Expands on Local File Inclusion by exploring additional scenarios, common filters, and techniques for analysing vulnerable implementations.

### 6. Remote File Inclusion (RFI)

Explains how applications that include remote resources may allow attackers to execute malicious code hosted on external systems.

### 7. Challenge

Applies all concepts learned throughout the room in a series of practical exercises focused on identifying and exploiting file inclusion vulnerabilities.

### 8. Remediation

Reviews defensive techniques, secure coding practices, and server-side configuration changes used to prevent file inclusion vulnerabilities.

---

## Skills Practiced

- Path Traversal
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)
- HTTP Request Analysis
- Web Application Security
- Input Validation
- Secure File Handling
- Vulnerability Assessment

---

## Tools Used

- Web Browser
- Burp Suite
- Browser Developer Tools
- TryHackMe AttackBox
- HTTP Requests

---

## Key Takeaways

- File Inclusion vulnerabilities occur when applications trust user-controlled file paths.
- Path Traversal, LFI, and RFI are closely related but differ in how files are accessed and processed.
- Unsafe server-side file inclusion may expose sensitive information or lead to remote code execution.
- Proper input validation, allowlists, secure server configuration, and careful use of file-handling functions are essential for preventing file inclusion vulnerabilities.
- Secure coding practices should always be combined with layered defensive controls to minimise risk. :contentReference[oaicite:1]{index=1} :contentReference[oaicite:2]{index=2}