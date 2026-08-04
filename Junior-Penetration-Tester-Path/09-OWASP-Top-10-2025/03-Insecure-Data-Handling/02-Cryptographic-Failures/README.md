# A04 - Cryptographic Failures

## Overview

**Cryptographic Failures** occur when sensitive information is not adequately protected because of weak encryption, insecure implementation, or poor cryptographic practices. Common examples include storing passwords without hashing, using outdated encryption algorithms, exposing encryption keys, or transmitting sensitive data without proper protection.

One of the most dangerous mistakes is attempting to **create custom cryptographic algorithms** instead of relying on well-tested, industry-standard implementations. Poor cryptographic design can expose confidential information even when developers believe data is protected.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Cryptographic Failures are
- Identify common cryptographic weaknesses
- Explain why modern cryptographic algorithms should be used
- Recognize insecure key management practices
- Apply secure cryptographic principles

---

## Main Content

### What are Cryptographic Failures?

Cryptographic Failures occur when applications fail to properly protect sensitive information.

Examples include:

- Passwords stored without hashing
- Weak or outdated encryption algorithms
- Exposed encryption keys
- Unencrypted sensitive communications

These weaknesses allow attackers to recover information that should remain confidential.

---

### Weak Cryptography

The room identifies several insecure cryptographic practices, including:

- Using outdated algorithms such as **MD5**
- Using **SHA-1**
- Using **DES**
- Poor implementation of encryption
- Weak protection of sensitive information

These algorithms are no longer considered secure for protecting sensitive data.

---

### Avoid Custom Cryptography

A common mistake is attempting to create custom encryption algorithms.

Instead of implementing proprietary cryptography, developers should always use:

- Industry-standard algorithms
- Well-tested cryptographic libraries
- Publicly reviewed implementations

Trusted libraries significantly reduce the risk of introducing cryptographic weaknesses.

---

### Secure Key Management

Protecting cryptographic keys is just as important as choosing strong algorithms.

Applications should never store:

- API credentials
- Encryption keys
- Secrets
- Access tokens

inside:

- Source code
- Configuration files
- Public repositories

Instead, dedicated secret management systems should be used.

---

### Preventing Cryptographic Failures

Recommended defensive practices include:

- Hash passwords using **bcrypt**, **scrypt**, or **Argon2**.
- Use modern, trusted cryptographic libraries.
- Never develop custom encryption algorithms.
- Store secrets in secure key management systems.
- Protect sensitive information during storage and transmission.

---

## Skills Practiced

- Cryptography
- Password Security
- Secret Management
- Secure Development
- Web Application Security

---

## Key Takeaways

- Cryptographic Failures occur when sensitive information is not properly protected.
- Weak algorithms such as MD5, SHA-1, and DES should no longer be used.
- Passwords should be hashed using modern algorithms like bcrypt, scrypt, or Argon2.
- Cryptographic keys and secrets should never be stored in source code or configuration files.
- Secure applications rely on trusted cryptographic libraries and proper key management rather than custom encryption implementations.