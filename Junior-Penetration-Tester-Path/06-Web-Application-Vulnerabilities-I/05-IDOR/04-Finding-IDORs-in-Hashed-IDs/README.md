# Finding IDORs in Hashed IDs

## Overview

Some web applications replace direct object identifiers with hashed values to make them less predictable. Although hashing obscures the original identifier, it does not provide access control. If the server accepts a valid hashed identifier without verifying whether the authenticated user is authorised to access the associated resource, the application remains vulnerable to Insecure Direct Object Reference (IDOR).

This lesson explains how hashed identifiers are used, why they should not be considered a security mechanism, and why proper server-side authorisation remains essential.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the purpose of hashed object identifiers
- Explain why hashing does not prevent IDOR vulnerabilities
- Recognise common hashing algorithms used in applications
- Understand the limitations of predictable identifiers
- Explain why authorisation is more important than identifier complexity

---

## Main Content

### What are Hashed IDs?

Some applications transform object identifiers using cryptographic hash functions before exposing them to users.

Common hashing algorithms include:

- MD5
- SHA-1
- SHA-256

The goal is often to hide sequential or easily predictable identifiers from users.

---

### Hashing vs Authorisation

Hashing changes the representation of an identifier but does not determine whether a user is allowed to access the corresponding resource.

If the server validates only the identifier and ignores ownership or permissions, the application remains vulnerable regardless of how the identifier is generated.

---

### Predictable Input

Applications that hash predictable values, such as sequential numbers, may still expose patterns that can be analysed during security assessments.

While hashing increases complexity compared to plain identifiers, it should never be treated as a replacement for proper access control.

Security depends on authorisation, not on how difficult an identifier is to recognise.

---

### Preventing IDOR

Applications should perform authorisation checks every time a protected resource is requested.

Effective access control should verify:

- The authenticated user
- Resource ownership
- User permissions
- Access control policies

Hashing may reduce identifier visibility, but it cannot prevent unauthorised access on its own.

---

## Skills Practiced

- IDOR Analysis
- Hashed Identifier Recognition
- Access Control Validation
- Web Application Security
- Secure Authorisation

---

## Key Takeaways

- Hashed identifiers obscure object references but do not enforce security.
- Predictable values should not rely on hashing as their primary protection.
- Every resource request requires server-side authorisation validation.
- Proper access control remains the only reliable defence against IDOR vulnerabilities involving hashed identifiers.