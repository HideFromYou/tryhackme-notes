# Identifying Hash Types

## Overview

Before attempting to crack a password hash, it is essential to identify the hashing algorithm that produced it. Using the wrong hash mode in **Hashcat** or the wrong format in **John the Ripper** will prevent the attack from succeeding, regardless of the quality of the wordlist or attack strategy.

This lesson explains how to recognize common hash types using their visual characteristics, identify unknown hashes with tools such as **hashid** and **Hashcat's `--identify`**, and map each algorithm to the correct cracking mode.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify common password hash formats
- Recognize hashes based on length and prefixes
- Use `hashid` to identify unknown hashes
- Use Hashcat's `--identify` feature
- Select the correct Hashcat mode and John the Ripper format
- Understand why context matters when identifying hashes

---

## Main Content

### Why Hash Identification Matters

Password cracking begins with identifying the hashing algorithm.

If the wrong algorithm is selected:

- Hashcat will use an incorrect mode.
- John the Ripper will use an incorrect format.
- The attack will fail even if the correct password exists in the wordlist.

Correct hash identification is therefore the first step in every offline password-cracking workflow.

---

### Visual Characteristics

Many hash types can be recognized by examining their length and format.

| Hash Type | Length | Identifier |
|-----------|--------|------------|
| **MD5** | 32 hexadecimal characters | No prefix |
| **SHA-1** | 40 hexadecimal characters | No prefix |
| **SHA-256** | 64 hexadecimal characters | No prefix |
| **NTLM** | 32 hexadecimal characters | No prefix |
| **bcrypt** | Approximately 60 characters | `$2a$`, `$2b$`, or `$2y$` |

The most common ambiguity occurs between **MD5** and **NTLM**, as both produce 32-character hexadecimal hashes.

In these cases, surrounding context often determines the correct algorithm.

For example:

- Hashes extracted from Windows systems are typically **NTLM**.
- Hashes recovered from web applications are more commonly **MD5** or a SHA variant.

---

### Identifying Hashes with hashid

The lesson introduces **hashid**, a utility that analyzes a hash and returns possible matching algorithms.

Example:

```bash
hashid '5f4dcc3b5aa765d61d8327deb882cf99'
```

For hashes that share similar formats, hashid returns multiple possible algorithms.

Penetration testers should combine these results with contextual information to determine the most likely candidate.

For bcrypt hashes, hashid provides an unambiguous identification because of the `$2a$`, `$2b$`, or `$2y$` prefix.

---

### Identifying Hashes with Hashcat

Hashcat includes its own identification feature:

```bash
hashcat --identify <hash>
```

Unlike hashid, Hashcat also displays the corresponding **Hashcat mode numbers**, making it easier to move directly into password cracking.

This provides a fast workflow from unknown hash to attack configuration.

---

### Online Hash Lookup Services

The lesson mentions several online lookup services capable of identifying or searching for previously cracked hashes.

These services may quickly recover common passwords using precomputed databases.

However, they should **never** be used with client hashes during real penetration tests because submitting hashes to third-party websites may expose sensitive information.

---

### Hashcat Modes and John Formats

Once the hash type has been identified, the correct mode or format must be selected.

| Algorithm | Hashcat Mode | John Format |
|-----------|-------------:|------------|
| **MD5** | `0` | `raw-md5` |
| **SHA-1** | `100` | `raw-sha1` |
| **SHA-256** | `1400` | `raw-sha256` |
| **SHA-512** | `1700` | `raw-sha512` |
| **NTLM** | `1000` | `nt` |
| **bcrypt** | `3200` | `bcrypt` |

Selecting the wrong mode is one of the most common reasons password-cracking attempts fail.

When multiple candidates exist, the lesson recommends trying the most likely algorithm first before testing alternatives.

---

## Skills Practiced

- Hash Identification
- Password Cracking Preparation
- hashid
- Hashcat
- John the Ripper
- Hash Analysis
- Offline Password Auditing

---

## Key Takeaways

- Correctly identifying the hashing algorithm is the first step before attempting password cracking.
- Hash length, prefixes, and contextual information help distinguish common hash formats.
- Tools such as **hashid** and **Hashcat's `--identify`** automate hash identification.
- Hashcat requires the correct **mode number**, while John the Ripper requires the correct **format**.
- Choosing the wrong algorithm prevents successful password recovery, even when the correct password exists in the wordlist.