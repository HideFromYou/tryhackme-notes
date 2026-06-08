# 🧪 TryHackMe Web Security Learning Notes

This repository contains structured notes from TryHackMe web security modules and challenges.  
The goal is to document offensive security concepts, attack surfaces, and methodology in a clean and professional way.

---

## 🎯 Covered Topics

### 🔹 SQL Injection Introduction
Understanding how unsanitized user input can manipulate SQL queries and lead to:
- Data extraction
- Authentication bypass
- Database enumeration

---

### 🔹 CSRF Introduction
Cross-Site Request Forgery concepts:
- Forced user actions without consent
- Session-based attack exploitation
- Importance of anti-CSRF tokens

---

### 🔹 XSS Introduction
Cross-Site Scripting fundamentals:
- Reflected XSS
- Stored XSS
- DOM-based XSS
- Session theft and client-side impact

---

### 🔹 SSRF Introduction
Server-Side Request Forgery basics:
- Forcing server-side requests
- Internal network discovery
- Cloud metadata exploitation risks

---

### 🔹 IDOR (Insecure Direct Object Reference)
- Accessing unauthorized resources
- Broken access control
- Object-level authorization flaws

---

### 🔹 Session Management
- Session cookies handling
- Session hijacking risks
- Weak session tokens
- Authentication persistence flaws

---

### 🔹 Broken Authentication
- Login bypass techniques (conceptual)
- Weak password policies
- Improper authentication logic
- Privilege escalation via auth flaws

---

### 🔹 File Inclusion
- Local File Inclusion (LFI)
- Remote File Inclusion (RFI)
- Path traversal vulnerabilities
- Sensitive file exposure risks

---

### 🔹 Command Injection
- Execution of system commands via web input
- Web-to-shell interaction
- Risk of full Remote Code Execution (RCE)

---

### 🔹 API Pentesting
- API enumeration and testing
- Broken object-level authorization (BOLA)
- Excessive data exposure
- Missing authentication controls

---

## 🧪 TryHackMe Challenges

### 🔥 Recruit Challenge
- Web-based enumeration and exploitation challenge
- Focus on identifying hidden attack surfaces
- Understanding application logic flaws
- Privilege escalation concepts inside application flow

---

### 🔥 Support Challenge
- Authenticated web application testing scenario
- Focus on:
  - Input handling flaws
  - Ticket system logic weaknesses
  - Potential RCE paths via application features
- Demonstrates attack chaining in real-world style applications

---

## 🧠 Methodology

1. Reconnaissance (identify entry points)
2. Enumeration of web application structure
3. Identification of input vectors
4. Testing for injection and logic flaws
5. Analysis of authentication/session mechanisms
6. Mapping privilege escalation paths
7. Assessing potential impact (data → system → RCE)

---

## 🎯 Security Mindset

- Never trust user input
- Focus on application logic, not just vulnerabilities
- Think in attack chains, not isolated bugs
- Understand how small flaws escalate into full compromise
- Evaluate both frontend and backend behavior

---

## ⚠️ Disclaimer

This repository is for educational purposes only and based on legal training environments (TryHackMe).

No real-world exploitation content is included.

---

## 🚀 Goal

To build a structured understanding of web application security and develop an offensive security mindset suitable for penetration testing roles.
