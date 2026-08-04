# A08 - Software or Data Integrity Failures

## Overview

**Software or Data Integrity Failures** occur when an application trusts software, updates, configuration files, or critical data **without verifying their authenticity, integrity, or origin**. Instead of confirming that code or data has not been modified, the application assumes it is safe, allowing attackers to introduce malicious content that affects application behavior.

These failures commonly involve unverified software updates, insecure deserialization, untrusted configuration files, or build processes that lack integrity verification. Because applications often rely on external components and automated deployment pipelines, maintaining trust boundaries is essential.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Software or Data Integrity Failures are
- Explain why integrity verification is important
- Recognize common integrity-related weaknesses
- Understand how insecure deserialization can be exploited
- Apply secure integrity verification practices

---

## Main Content

### What are Software or Data Integrity Failures?

Software or Data Integrity Failures occur when applications trust software or data without verifying that it is authentic and has not been altered.

Examples include:

- Unverified software updates
- Untrusted configuration files
- Unsigned binaries
- Modified templates
- Tampered JSON files

Without integrity verification, attackers may introduce malicious content into trusted workflows.

---

### Why Integrity Matters

Applications depend on trusted software and data to operate correctly.

If attackers can modify:

- Application updates
- Configuration files
- Executable code
- Serialized objects
- Critical application data

they may influence application behavior or execute malicious code.

Trust should always be established through verification rather than assumption.

---

### Common Integrity Failures

The room highlights several examples:

- Trusting software updates without verification
- Loading scripts from untrusted sources
- Failing to validate configuration files
- Accepting modified binaries or templates
- Processing serialized data without verification

Each example demonstrates the dangers of assuming data is trustworthy simply because it is received by the application.

---

### Insecure Deserialization

The practical exercise demonstrates an **insecure deserialization** attack using Python.

Applications that deserialize untrusted data without validation may execute attacker-controlled objects or logic, potentially leading to arbitrary code execution or unauthorized access.

This illustrates why serialized data should never be trusted without proper validation.

---

### Preventing Integrity Failures

Recommended defensive practices include:

- Verify software updates before installation.
- Use cryptographic checksums and digital signatures.
- Restrict modification of critical application files.
- Validate serialized data before processing.
- Establish trust boundaries throughout CI/CD pipelines.
- Accept software and data only from trusted sources.

---

## Skills Practiced

- Software Integrity
- Data Integrity
- Insecure Deserialization
- Secure Software Development
- CI/CD Security
- Web Application Security

---

## Key Takeaways

- Software or Data Integrity Failures occur when applications trust code or data without verifying its authenticity or integrity.
- Software updates, configuration files, binaries, templates, and serialized objects should all be verified before use.
- Insecure deserialization allows attacker-controlled serialized data to influence application behavior.
- Cryptographic verification, trusted sources, and secure CI/CD processes help maintain software integrity.
- Applications should verify trust rather than assume it, reducing the risk of malicious software or data entering the environment.