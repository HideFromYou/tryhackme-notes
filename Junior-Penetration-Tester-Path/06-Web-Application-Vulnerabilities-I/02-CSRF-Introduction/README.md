# CSRF Introduction

## Overview

Cross-Site Request Forgery (CSRF) is a web application vulnerability that allows an attacker to trick an authenticated user into performing unintended actions on a trusted website. Because the victim's browser automatically includes valid authentication credentials, the server may process malicious requests as if they were legitimate.

This room introduces the core concepts behind CSRF, explains why these attacks succeed, explores common exploitation scenarios, and presents defensive mechanisms used to protect modern web applications.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand how Cross-Site Request Forgery attacks work
- Explain why authenticated sessions are vulnerable to CSRF
- Identify common indicators of CSRF vulnerabilities
- Understand the role of CSRF tokens and other defensive mechanisms
- Recognise best practices for preventing CSRF attacks
- Develop a methodology for assessing CSRF vulnerabilities

---

## Lessons

1. Introduction
2. What is CSRF?
3. Why CSRF Works
4. Finding CSRF Vulnerabilities
5. Exploitation Using HTML Forms
6. Exploitation Over Weak Tokens
7. Best Practices
8. Conclusion

---

## Skills Practiced

- CSRF Fundamentals
- Session Security
- Web Application Security
- Vulnerability Identification
- CSRF Mitigation
- Secure Application Design

---

## Tools Used

- Web Browser
- Browser Developer Tools
- HTML Forms
- HTTP Requests
- TryHackMe Lab Environment

---

## Key Takeaways

- CSRF exploits the trust a web application places in an authenticated user's browser.
- Authentication alone does not protect applications from forged requests.
- Proper CSRF protections require secure request validation rather than relying solely on user sessions.
- Multiple defensive controls work together to reduce the risk of CSRF attacks.
- Understanding both attack techniques and mitigation strategies is essential for effective web application security testing.