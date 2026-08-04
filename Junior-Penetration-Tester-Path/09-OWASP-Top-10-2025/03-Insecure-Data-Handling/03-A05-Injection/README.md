# A05 - Injection

## Overview

**Injection** vulnerabilities occur when an application treats untrusted user input as part of a command or query. Instead of processing the input as ordinary data, the application interprets it as executable instructions, allowing attackers to manipulate the application's behavior.

Injection attacks remain one of the most dangerous web application vulnerabilities because they can lead to unauthorized data access, authentication bypass, remote code execution, or complete system compromise. Modern applications must validate and safely handle every piece of user-controlled input before using it.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Injection vulnerabilities are
- Explain how Injection attacks occur
- Identify common Injection attack types
- Recognize the risks of trusting user input
- Apply secure input handling techniques

---

## Main Content

### What is Injection?

Injection occurs when an application inserts user-controlled input into commands, queries, or interpreters without proper validation or sanitization.

Instead of treating the input as data, the interpreter executes part of the supplied input as code or instructions.

---

### Why Injection Matters

Applications constantly process user input through:

- Search fields
- Login forms
- URL parameters
- API requests
- File uploads

If this input is not handled safely, attackers can modify how the application behaves or access resources they should not control.

---

### Common Injection Attacks

Modern applications may be vulnerable to several Injection attacks, including:

- SQL Injection (SQLi)
- Command Injection
- LDAP Injection
- XML Injection
- Server-Side Template Injection (SSTI)
- AI Prompt Injection

Although each targets a different interpreter, they all exploit the same underlying problem: untrusted input reaching an interpreter without proper validation.

---

### Preventing Injection

Applications should:

- Validate all user input.
- Use parameterized queries.
- Avoid constructing commands through string concatenation.
- Escape special characters where appropriate.
- Apply input validation on the server.
- Follow the principle of least privilege.

Treat every piece of user-controlled input as untrusted until it has been properly validated.

---

## Skills Practiced

- Input Validation
- Injection Prevention
- Secure Coding
- Web Application Security
- OWASP Top 10

---

## Key Takeaways

- Injection vulnerabilities occur when applications execute untrusted user input.
- SQL Injection, Command Injection, SSTI, and Prompt Injection all result from unsafe input handling.
- Applications should separate data from executable commands through parameterized queries and secure APIs.
- Server-side validation is essential because client-side controls can be bypassed.
- Proper input validation significantly reduces the risk of Injection attacks.