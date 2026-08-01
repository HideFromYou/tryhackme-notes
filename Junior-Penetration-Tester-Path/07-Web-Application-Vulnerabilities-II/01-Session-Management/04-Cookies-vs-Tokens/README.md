# Cookies vs Tokens

## Overview

Modern web applications primarily manage authenticated sessions using either cookies or tokens. Both approaches allow applications to identify users across multiple HTTP requests, but they differ in how session information is stored, transmitted, and protected.

This lesson compares cookie-based and token-based session management, explains how each method works, and highlights their advantages, limitations, and common security considerations.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the differences between cookies and tokens
- Explain how cookie-based session management works
- Explain how token-based session management works
- Recognise the advantages and disadvantages of each approach
- Understand common security mechanisms used to protect sessions

---

## Main Content

### Cookie-Based Session Management

In cookie-based authentication, the server creates a session and sends a session identifier to the browser using the **Set-Cookie** HTTP response header.

The browser stores the cookie and automatically includes it with future requests to the same application.

Common cookie security attributes include:

- **Secure** – Sends the cookie only over HTTPS connections.
- **HttpOnly** – Prevents client-side JavaScript from accessing the cookie.
- **Expires** – Defines when the cookie becomes invalid.
- **SameSite** – Restricts cross-site transmission to help reduce CSRF attacks.

Because browsers manage cookies automatically, no additional client-side logic is required to attach them to requests.

---

### Token-Based Session Management

In token-based authentication, the server returns a token after successful authentication.

The client application stores the token, commonly in browser storage, and manually includes it with future requests.

A common implementation uses **JSON Web Tokens (JWTs)** transmitted in the:

```http
Authorization: Bearer <token>
```

HTTP request header.

Unlike cookies, browsers do not automatically send tokens with requests.

---

### Comparing Cookies and Tokens

| Cookie-Based Sessions | Token-Based Sessions |
|------------------------|----------------------|
| Automatically sent by the browser | Added manually by the client application |
| Built-in browser security attributes | Security depends on application implementation |
| Simple for traditional web applications | Well suited for APIs and modern SPAs |
| Can be vulnerable to CSRF without proper protections | Naturally resistant to traditional CSRF because browsers do not attach tokens automatically |

Each approach has strengths and trade-offs depending on the application's architecture.

---

### Security Considerations

Regardless of the session mechanism used, applications should:

- Protect session values from disclosure
- Use HTTPS for all authenticated communication
- Implement secure expiration policies
- Validate session information on every request
- Apply appropriate access control checks

The security of the session depends more on its implementation than on whether cookies or tokens are used.

---

## Skills Practiced

- Cookie-Based Authentication
- Token-Based Authentication
- Session Security
- HTTP Security
- Web Application Security

---

## Key Takeaways

- Cookies and tokens both provide mechanisms for maintaining authenticated sessions.
- Cookies are automatically managed by the browser and support built-in security attributes.
- Tokens are managed by the client application and commonly transmitted using the `Authorization: Bearer` header.
- Both approaches require secure implementation to protect authenticated user sessions.
- Proper session validation and access control remain essential regardless of the chosen authentication mechanism.