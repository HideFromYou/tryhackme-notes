# Remediation – Sanitisation

## Overview

Preventing Command Injection requires applications to ensure that user-controlled input can never alter the operating system commands executed by the server. Simply filtering dangerous characters is rarely sufficient, as attackers often discover alternative ways to manipulate command execution. Effective protection relies on secure input validation, sanitisation, safe APIs, and the principle of least privilege.

This lesson examines secure coding practices used to prevent Command Injection vulnerabilities and explains why defence in depth is essential when interacting with operating system commands.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand why input sanitisation alone is insufficient
- Explain secure methods for validating user input
- Recognise safe alternatives to executing shell commands
- Understand the importance of least privilege
- Apply secure coding practices to prevent Command Injection

---

## Main Content

### Validate User Input

Applications should never trust user-controlled input.

Whenever possible:

- Accept only expected values
- Reject unexpected characters
- Use allowlists instead of blocklists
- Validate input before processing

Strict validation greatly reduces opportunities for command injection.

---

### Avoid Shell Execution

Whenever possible, applications should avoid invoking operating system shells entirely.

Instead of building shell commands using string concatenation, developers should:

- Use language-specific APIs
- Use system libraries
- Call application functions directly
- Avoid passing user input to shell interpreters

Eliminating shell execution removes the primary attack surface.

---

### Sanitise User Input

If operating system commands cannot be avoided, user input should be sanitised before being processed.

Sanitisation should:

- Escape special shell characters
- Remove dangerous input
- Restrict command arguments
- Prevent shell operator injection

Sanitisation should always be combined with strict input validation.

---

### Principle of Least Privilege

Applications should execute with the minimum permissions necessary.

Limiting privileges reduces the potential impact if Command Injection occurs.

Recommended practices include:

- Non-administrative service accounts
- Restricted filesystem permissions
- Limited operating system privileges
- Process isolation

Even if exploitation succeeds, least privilege helps minimise damage.

---

### Defence in Depth

Effective Command Injection prevention combines multiple security controls:

- Input validation
- Input sanitisation
- Parameterised APIs
- Avoiding shell execution
- Least privilege
- Security monitoring
- Regular code reviews

No single mitigation completely eliminates Command Injection risk.

---

## Skills Practiced

- Input Validation
- Input Sanitisation
- Secure Coding
- Least Privilege
- Command Injection Prevention
- Web Application Security

---

## Key Takeaways

- Input validation should always occur before user data reaches operating system commands.
- Avoiding shell execution is more secure than attempting to sanitise dangerous input.
- Sanitisation complements—but does not replace—proper validation.
- Applications should run with the minimum privileges required.
- Layered security controls provide the strongest defence against Command Injection vulnerabilities.