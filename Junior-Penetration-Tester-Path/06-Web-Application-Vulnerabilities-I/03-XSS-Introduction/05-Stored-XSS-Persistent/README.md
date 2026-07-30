# Stored XSS (Persistent)

## Overview

Stored Cross-Site Scripting (Stored XSS), also known as Persistent XSS, occurs when malicious user input is permanently stored by a web application and later delivered to other users. Unlike Reflected XSS, the malicious content remains on the server until it is retrieved and rendered by a victim's browser.

This lesson explains how Stored XSS works, why it is often considered more severe than Reflected XSS, and the security practices that help prevent persistent client-side code injection.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how Stored XSS differs from Reflected XSS
- Explain why persistent user input creates additional security risks
- Identify common locations where Stored XSS may occur
- Understand the potential impact on multiple users
- Recognise defensive measures used to prevent Stored XSS

---

## Main Content

### What is Stored XSS?

Stored XSS occurs when a web application saves user-controlled input and later displays it to other users without properly validating or encoding the content.

When the stored data is rendered by a browser, it may be interpreted as executable JavaScript instead of plain text.

---

### Where Stored XSS Appears

Persistent XSS vulnerabilities commonly affect features that permanently store user-generated content.

Examples include:

- User profiles
- Comment sections
- Forums
- Support tickets
- Chat systems
- Product reviews

Any feature that accepts and later displays user input should be considered a potential attack surface.

---

### Why Stored XSS Is More Dangerous

Unlike Reflected XSS, Stored XSS does not require victims to visit a specially crafted link.

Once malicious content is stored by the application, every user who accesses the affected page may automatically receive the payload.

This makes Stored XSS capable of affecting multiple users over an extended period until the malicious content is removed.

---

### Preventing Stored XSS

Applications should treat all stored user input as untrusted.

Effective defensive measures include:

- Validating user input
- Applying context-aware output encoding
- Sanitising rich user-generated content where appropriate
- Implementing Content Security Policy (CSP)
- Performing regular security testing

Applying multiple layers of protection significantly reduces the likelihood of persistent client-side code execution.

---

## Skills Practiced

- Stored XSS Fundamentals
- Client-Side Security
- Secure Input Handling
- Output Encoding Concepts
- Web Application Security

---

## Key Takeaways

- Stored XSS occurs when malicious input is permanently saved by an application.
- Every user who views the affected content may be exposed to the vulnerability.
- Persistent XSS often presents a greater risk than reflected XSS because it can affect multiple victims automatically.
- Proper input validation, output encoding, and secure development practices are essential for preventing Stored XSS.