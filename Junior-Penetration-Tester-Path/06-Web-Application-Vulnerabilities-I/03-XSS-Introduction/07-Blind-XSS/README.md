# Blind XSS

## Overview

Blind Cross-Site Scripting (Blind XSS) is a form of persistent XSS in which malicious input is submitted to a web application but executes later in a different user's browser, often within internal administrative interfaces. Unlike other XSS variants, the attacker may not immediately observe whether the payload has been executed, making detection and assessment more challenging.

This lesson introduces Blind XSS, explains how delayed execution occurs, and highlights why secure handling of user-generated content is essential throughout an application.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Blind XSS is
- Explain how Blind XSS differs from other XSS variants
- Recognise scenarios where delayed execution may occur
- Understand the security risks associated with administrative interfaces
- Identify defensive measures that help prevent Blind XSS

---

## Main Content

### What is Blind XSS?

Blind XSS occurs when malicious input is accepted and stored by an application but executes later in a different part of the system.

The attacker does not immediately see the result, making the vulnerability more difficult to identify than Reflected or Stored XSS.

---

### Delayed Execution

Blind XSS commonly appears when submitted content is later viewed by privileged users.

Examples include:

- Administrative dashboards
- Support ticket systems
- Log viewers
- Moderation panels
- Internal management portals

When this stored content is rendered without appropriate protection, the browser may execute it as active JavaScript.

---

### Why Blind XSS Is Dangerous

Blind XSS can have a significant impact because it often targets users with elevated privileges.

Potential consequences include:

- Exposure of sensitive information
- Execution of actions within privileged sessions
- Compromise of administrative functionality
- Increased attack surface across internal systems

The delayed nature of the vulnerability can also make detection more difficult during routine testing.

---

### Preventing Blind XSS

Applications should apply consistent security controls wherever user-generated content is displayed.

Effective mitigation includes:

- Validating user input
- Applying context-aware output encoding
- Sanitising untrusted content
- Using Content Security Policy (CSP)
- Following secure coding practices across both public and internal interfaces

Security controls should be applied consistently, regardless of who views the content.

---

## Skills Practiced

- Blind XSS Fundamentals
- Client-Side Security
- Secure Input Handling
- Administrative Interface Security
- Web Application Security

---

## Key Takeaways

- Blind XSS executes after malicious content is viewed in a different part of an application.
- The attacker may not receive immediate confirmation that the payload has executed.
- Administrative and internal interfaces are common locations where Blind XSS may appear.
- Consistent input validation, output encoding, and layered security controls help prevent Blind XSS vulnerabilities.