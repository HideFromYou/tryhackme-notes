# Cross-Site Scripting (XSS) Notes

## Overview

Cross-Site Scripting (XSS) is a web application vulnerability where untrusted user-controlled input is executed as JavaScript in another user's browser.

Potential impact:

- JavaScript execution in victim browser
- Session hijacking concepts
- DOM manipulation
- Credential theft concepts
- Client-side forced actions
- Business logic abuse

---

## Types of XSS

### Reflected XSS

Occurs when user-controlled input from an HTTP request is reflected in the server response without proper sanitization or output encoding.

Flow:

User request → server reflects input → browser executes payload

Example:

Direct HTML reflection:

```html
<p>Hello USER_INPUT</p>
```

Proof of concept payload:

```html
<script>alert('XSS')</script>
```

If input is reflected inside an HTML attribute:

```html
<input value="USER_INPUT">
```

payload must break out of the attribute context:

```html
"><script>alert('XSS')</script>
```

Key lesson:

Payload construction depends on where the input is reflected in the HTML context.

---

### Stored XSS

Occurs when malicious input is stored server-side and later executed when another user loads the affected content.

Examples:

- comments
- profile fields
- messages
- support tickets

---

### DOM-Based XSS

Occurs when client-side JavaScript processes unsafe user input and writes it into the DOM without proper sanitization.

Client-side source-to-sink issue.

---

### Blind XSS

Blind XSS occurs when payload execution happens in a context the attacker cannot directly observe.

Examples:

- admin dashboards
- support interfaces
- moderation panels
- backend review systems

Key lesson:

Execution may occur later in a different user context.

---

## Practical Learning

Hands-on concepts practiced:

- reflected XSS payload testing
- proof-of-concept payload validation
- HTML context escaping
- attribute breakout payload construction
- blind XSS concepts
- browser page source inspection

---

## Tools Used

- Browser Developer Tools / View Page Source
- TryHackMe labs
