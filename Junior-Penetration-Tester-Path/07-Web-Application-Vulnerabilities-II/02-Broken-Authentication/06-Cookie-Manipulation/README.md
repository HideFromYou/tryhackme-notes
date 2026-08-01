# Cookie Manipulation

## Overview

Cookies are widely used by web applications to maintain authenticated user sessions across multiple HTTP requests. Because browsers automatically include cookies with subsequent requests, the server often relies on their contents when making authentication and authorisation decisions. If cookie values can be modified without verification, attackers may be able to impersonate other users or elevate their privileges. :contentReference[oaicite:0]{index=0}

This lesson examines insecure cookie implementations, explains common cookie formats, and demonstrates why cookies must always be protected with integrity mechanisms rather than relying on obscurity. :contentReference[oaicite:1]{index=1}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how cookies are used for authentication
- Recognise insecure cookie implementations
- Differentiate between plain text, hashed, and encoded cookies
- Explain why hashing or encoding does not provide integrity
- Understand secure approaches for protecting authentication cookies

---

## Main Content

### Cookies and Authentication

HTTP is a stateless protocol, so web applications commonly use cookies to remember authenticated users across requests.

When authentication information is stored inside a cookie, the server must verify that the cookie has not been modified before trusting its contents. Otherwise, attackers may be able to change authentication-related values. :contentReference[oaicite:2]{index=2}

---

### Plain Text Cookies

Plain text cookies store authentication or authorisation information directly within the cookie.

Examples may include values representing:

- Login status
- User roles
- Administrative privileges

If these values are accepted without integrity verification, a client can modify them and potentially change how the application interprets the session. :contentReference[oaicite:3]{index=3}

---

### Hashed Cookies

Some applications store hashed values inside cookies under the assumption that hashing prevents tampering.

However, hashing alone does not provide authenticity or integrity.

If an attacker knows or can determine the original value, they can generate the corresponding hash and replace the cookie value. A hash proves only what data was hashed—it does not prove who created it. :contentReference[oaicite:4]{index=4}

---

### Encoded Cookies

Encoding transforms data into another representation so it can be transported safely through protocols such as HTTP.

Common encodings include:

- Base64
- Base32

Encoding is completely reversible and provides:

- No confidentiality
- No integrity
- No authentication

If encoded cookie data is not protected, it can be decoded, modified, re-encoded, and accepted by the application. :contentReference[oaicite:5]{index=5}

---

### Secure Cookie Protection

Authentication cookies should be protected using integrity mechanisms rather than relying on hidden values.

Recommended approaches include:

- Cryptographic signatures
- HMAC
- Signed JSON Web Tokens (JWTs)
- Opaque session identifiers with server-side session storage

These mechanisms allow the server to detect unauthorised modifications before accepting a cookie. :contentReference[oaicite:6]{index=6}

---

## Skills Practiced

- Cookie Security
- Authentication Security
- Session Management
- Cookie Integrity
- Web Application Security

---

## Key Takeaways

- Authentication cookies must never be trusted without server-side integrity verification.
- Plain text, hashed, and encoded cookies can all be manipulated if they are not properly protected.
- Hashing and encoding do not provide authenticity or tamper protection.
- Cryptographic signing or server-side session storage are the recommended approaches for protecting authentication cookies. :contentReference[oaicite:7]{index=7} :contentReference[oaicite:8]{index=8}