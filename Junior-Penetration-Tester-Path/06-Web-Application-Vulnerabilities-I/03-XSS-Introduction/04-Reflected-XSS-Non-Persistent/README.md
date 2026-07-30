# Reflected XSS (Non-Persistent)

## Overview

Reflected Cross-Site Scripting (Reflected XSS) is a type of XSS vulnerability where user-supplied input is immediately included in a server's response without proper sanitisation or output encoding. The malicious content is not stored by the application but is reflected back to the user's browser, where it may be executed.

This lesson explains how reflected XSS occurs, the conditions required for exploitation, and why proper handling of user input is essential for preventing client-side code injection.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how Reflected XSS works
- Explain why reflected input creates security risks
- Recognise common locations where reflected XSS may occur
- Understand the impact of client-side code execution
- Identify defensive measures used to prevent reflected XSS

---

## Main Content

### What is Reflected XSS?

Reflected XSS occurs when an application immediately returns user-controlled input within an HTTP response without treating it as untrusted data.

Because the malicious content is not stored on the server, the attack typically requires the victim to submit or visit a specially crafted request.

---

### How Reflection Happens

Applications commonly reflect user input when displaying:

- Search results
- Error messages
- Login feedback
- Form validation messages
- URL parameters

If reflected data is rendered without appropriate output encoding, browsers may interpret it as executable JavaScript instead of plain text.

---

### Characteristics of Reflected XSS

Reflected XSS generally has several defining characteristics:

- The payload is **not** stored by the application.
- The malicious input is processed immediately.
- User interaction is usually required.
- Execution occurs within the victim's browser.

These characteristics distinguish reflected XSS from persistent forms of the vulnerability.

---

### Preventing Reflected XSS

Effective protection involves treating all user input as untrusted.

Common defensive measures include:

- Validating user input
- Applying context-aware output encoding
- Using secure templating frameworks
- Implementing Content Security Policy (CSP)
- Following secure development practices

Combining multiple layers of defence significantly reduces the likelihood of reflected XSS vulnerabilities.

---

## Skills Practiced

- Reflected XSS Fundamentals
- Client-Side Security
- HTTP Response Analysis
- Input Validation Concepts
- Web Application Security

---

## Key Takeaways

- Reflected XSS occurs when untrusted input is immediately returned in a server response.
- The malicious content is not permanently stored by the application.
- Browsers may execute reflected input if it is not properly encoded.
- Context-aware output encoding and secure input handling are essential for preventing reflected XSS.