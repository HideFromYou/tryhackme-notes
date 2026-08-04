# AS04 - Cryptographic Failures

## Overview

**Cryptographic Failures** occur when encryption is implemented incorrectly or not used where it is required. Weak algorithms, hard-coded secrets, poor key management, or unencrypted sensitive data can allow attackers to recover confidential information such as passwords, tokens, personal data, or cryptographic keys.

Modern web applications rely on cryptography to protect data both **in transit** and **at rest**. When these protections fail, attackers may perform man-in-the-middle attacks, brute-force weak encryption, or simply recover secrets that were never properly protected. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Cryptographic Failures are
- Identify common cryptographic weaknesses
- Explain why proper key management is essential
- Recognize insecure cryptographic implementations
- Apply cryptographic security best practices

---

## Main Content

### What are Cryptographic Failures?

Cryptographic Failures occur when applications fail to properly protect sensitive information through encryption.

Examples include:

- Weak encryption algorithms
- Hard-coded secrets
- Poor key management
- Missing encryption

These weaknesses expose confidential information that should remain protected. :contentReference[oaicite:1]{index=1}

---

### Why Cryptography Matters

Cryptography protects many critical aspects of modern applications, including:

- Network communications
- Stored data
- User identities
- Passwords
- Authentication tokens
- Sensitive secrets

If these protections fail, attackers may gain unauthorized access to sensitive information or compromise user accounts. :contentReference[oaicite:2]{index=2}

---

### Common Cryptographic Weaknesses

The room highlights several common failures:

- Deprecated algorithms such as **MD5** and **SHA-1**
- ECB encryption mode
- Hard-coded secrets
- Poor key rotation
- Weak key management
- Missing encryption for data at rest or in transit
- Invalid or self-signed TLS certificates
- AI/ML systems exposing sensitive parameters or secrets :contentReference[oaicite:3]{index=3}

---

### Common Attack Scenarios

Attackers may exploit cryptographic weaknesses through:

- Man-in-the-Middle (MitM) attacks
- Brute-force attacks against weak keys
- Recovery of hard-coded secrets
- Accessing data that was never encrypted

Improper cryptography often exposes information without requiring exploitation of application logic. :contentReference[oaicite:4]{index=4}

---

### Preventing Cryptographic Failures

Recommended defensive practices include:

- Use modern algorithms such as **AES-GCM** or **ChaCha20-Poly1305**.
- Enforce **TLS 1.3** with valid certificates.
- Store secrets using dedicated key management services.
- Rotate keys and secrets regularly.
- Maintain an inventory of certificates and cryptographic keys.
- Ensure AI systems do not expose sensitive secrets or parameters. :contentReference[oaicite:5]{index=5}

---

## Skills Practiced

- Cryptography
- Key Management
- TLS Security
- Secret Management
- Secure Data Protection
- Web Application Security

---

## Key Takeaways

- Cryptographic Failures occur when encryption is weak, misconfigured, or absent.
- Hard-coded secrets and poor key management significantly increase security risk.
- Strong cryptography depends on both modern algorithms and secure operational practices.
- Sensitive data should always be protected both in transit and at rest.
- Effective cryptographic security requires secure key management, regular rotation, and continuous protection of secrets. :contentReference[oaicite:6]{index=6}