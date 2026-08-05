# How Passwords Are Stored

## Overview

Modern systems should never store passwords in plain text. Instead, they store a **cryptographic hash** of each password. During authentication, the user's submitted password is hashed and compared with the stored hash. If both values match, access is granted without ever storing or revealing the original password.

This lesson explains the properties of cryptographic hash functions, compares common hashing algorithms, introduces **salting**, and demonstrates why secure password storage is essential for defending against offline password-cracking attacks.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand why passwords should never be stored in plain text
- Explain how password hashing works
- Describe the key properties of cryptographic hash functions
- Compare common password hashing algorithms
- Understand the purpose of salting
- Recognize the security impact of poor password storage practices

---

## Main Content

### Plain Text Password Storage

Storing passwords in plain text is a critical security failure.

If an attacker gains access to the database, every password is immediately exposed without requiring any cracking.

Modern authentication systems instead store a **hash** of each password rather than the password itself.

---

### Password Verification

When a user logs in:

1. The user enters a password.
2. The application hashes the submitted password.
3. The generated hash is compared with the stored hash.
4. If both hashes match, authentication succeeds.

The original password never needs to be stored by the application.

---

### Properties of Cryptographic Hash Functions

A cryptographic hash function is suitable for password storage because it provides several important properties.

#### One-Way

A hash cannot be reversed to recover the original password.

The only practical approach is to hash candidate passwords and compare the results.

---

#### Deterministic

The same input always produces the same output.

For example, hashing the same password will always generate the identical hash value.

---

#### Fixed-Length Output

Regardless of password length, each algorithm always produces an output of a fixed size.

Examples include:

- MD5 → 32 hexadecimal characters
- SHA-1 → 40 hexadecimal characters
- SHA-256 → 64 hexadecimal characters

---

#### Collision Resistance

A secure hash function should make it computationally infeasible for two different inputs to produce the same output.

Algorithms that lose this property are no longer considered secure for password storage.

---

### Common Hashing Algorithms

The lesson compares several commonly encountered algorithms.

| Algorithm | Suitable for Password Storage | Notes |
|----------|------------------------------|------|
| MD5 | No | Fast and vulnerable to collisions |
| SHA-1 | No | Deprecated and considered insecure |
| SHA-256 | Sometimes | Better than MD5 but still very fast |
| NTLM | Legacy Windows | Based on MD4 |
| bcrypt | Yes | Slow and cost-configurable |
| Argon2 | Yes | Modern, memory-hard algorithm |

The key difference is **speed**.

Algorithms such as MD5, SHA-1, and SHA-256 were designed for integrity verification rather than password storage, while bcrypt and Argon2 intentionally slow password verification to resist brute-force attacks.

---

### Salting

A **salt** is a unique random value generated for each password before hashing.

Conceptually:

```text
stored_value = hash(password + salt)
```

Using unique salts ensures:

- Identical passwords produce different hashes.
- Rainbow table attacks become ineffective.
- Attackers cannot reuse precomputed hash databases.

Modern algorithms such as **bcrypt** and **Argon2** automatically generate, store, and manage salts internally.

---

### Password Storage Failures

The lesson highlights two real-world examples of insecure password storage.

#### RockYou Breach (2009)

Approximately 32 million passwords were stored in **plain text**, allowing immediate exposure after the database leak.

The resulting **rockyou.txt** wordlist remains one of the most widely used password dictionaries during penetration testing.

---

#### Aptoide Breach (2020)

Over 20 million accounts were protected using **unsalted SHA-1** hashes.

Because SHA-1 is extremely fast and lacked salting, attackers could recover many passwords rapidly using dictionary attacks and rainbow tables.

---

## Skills Practiced

- Password Hashing
- Password Storage
- Cryptographic Hash Functions
- Salting
- Hash Algorithms
- Password Security

---

## Key Takeaways

- Passwords should never be stored in plain text.
- Authentication systems store password hashes rather than original passwords.
- Secure hash functions are one-way, deterministic, fixed-length, and collision-resistant.
- Modern password hashing algorithms such as **bcrypt** and **Argon2** are designed to be slow, making brute-force attacks significantly more expensive.
- Salting ensures identical passwords generate different hashes and prevents rainbow table attacks.
- Weak algorithms and poor storage practices have contributed to major real-world password breaches.