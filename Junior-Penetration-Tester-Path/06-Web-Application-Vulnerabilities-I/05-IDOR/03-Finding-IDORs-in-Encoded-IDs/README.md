# Finding IDORs in Encoded IDs

## Overview

Some web applications encode object identifiers before sending them to the client in an attempt to make them less obvious. While encoding changes the appearance of an identifier, it does not provide access control or security. If the server still accepts the decoded value without verifying the user's permissions, the application remains vulnerable to Insecure Direct Object Reference (IDOR).

This lesson explains why encoded identifiers should not be considered a security mechanism and highlights the importance of proper server-side authorisation.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the purpose of encoded object identifiers
- Explain why encoding does not prevent IDOR vulnerabilities
- Recognise common forms of encoded identifiers
- Understand the importance of server-side authorisation
- Identify secure approaches to protecting application resources

---

## Main Content

### What are Encoded IDs?

Some applications encode identifiers before including them in requests or URLs.

Common reasons include:

- Improving readability
- Hiding sequential values
- Standardising data formats
- Reducing direct exposure of internal identifiers

Although the identifier appears different, the underlying value remains unchanged after decoding.

---

### Encoding Is Not Security

Encoding simply transforms data into another representation.

It does **not**:

- Verify user permissions
- Restrict access to resources
- Protect sensitive information
- Replace access control mechanisms

If the server accepts an encoded identifier without validating ownership, the application remains vulnerable to IDOR.

---

### Recognising Encoded Identifiers

Encoded identifiers may appear in various formats depending on the application.

Examples include:

- Base64-encoded values
- URL-encoded strings
- Hexadecimal representations
- Custom encoding schemes

Regardless of the format used, encoding should never be relied upon as a security control.

---

### Preventing IDOR with Encoded IDs

Applications should always validate whether the authenticated user is authorised to access the requested resource after processing the identifier.

Effective protection includes:

- Server-side authorisation checks
- Resource ownership validation
- Role-based access control
- Consistent permission enforcement

Encoding may improve usability or presentation, but it must never replace proper access control.

---

## Skills Practiced

- IDOR Analysis
- Encoded Identifier Recognition
- Access Control Validation
- Web Application Security
- Secure Authorisation

---

## Key Takeaways

- Encoded identifiers are an obfuscation technique, not a security mechanism.
- Decoding an identifier should always be followed by server-side authorisation checks.
- Access control must be enforced regardless of how object identifiers are represented.
- Proper authorisation is the only reliable defence against IDOR vulnerabilities involving encoded identifiers.