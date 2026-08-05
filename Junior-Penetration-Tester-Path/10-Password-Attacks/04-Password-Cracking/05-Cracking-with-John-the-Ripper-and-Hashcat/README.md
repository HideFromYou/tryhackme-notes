# Cracking with John the Ripper and Hashcat

## Overview

After identifying the hash type and selecting an attack strategy, the next step is performing the actual password-cracking attack. This lesson introduces **John the Ripper** and **Hashcat**, the two most widely used offline password-cracking tools. Both support dictionary, rule-based, and mask attacks, but differ in their performance, format handling, and primary use cases.

The lesson demonstrates how to configure each tool, perform common attack types, manage cracked passwords, and choose the most appropriate tool for different scenarios. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Perform dictionary attacks with John the Ripper
- Perform dictionary attacks with Hashcat
- Apply rule-based attacks using both tools
- Execute mask attacks with Hashcat
- View previously cracked passwords
- Understand the strengths of John the Ripper and Hashcat

---

## Main Content

### Preparing the Hashes

Before beginning the attacks, the lesson creates several files containing example **MD5** hashes.

Each file is used to demonstrate a different cracking technique:

- Dictionary attack
- Rule-based attack
- Mask attack

Organizing hashes into separate files allows each attack to focus on a specific technique. :contentReference[oaicite:1]{index=1}

---

### John the Ripper

John the Ripper is a CPU-based password cracker that supports numerous hash formats.

It is particularly useful for:

- Automatic hash format detection
- Unix password hashes
- Shadow files
- Quick password-cracking attempts

---

#### Dictionary Attacks

A basic dictionary attack uses:

- The hash format
- A wordlist
- A file containing hashes

John compares every word from the wordlist against the supplied hashes until a match is found.

Whenever the algorithm is known, explicitly specifying the correct `--format` improves reliability and avoids incorrect automatic detection.

---

#### Automatic Format Detection

John can automatically detect hash formats when no format is specified.

However, incorrect detection may result in:

- Wrong hash algorithm
- Zero recovered passwords
- Wasted cracking time

Whenever possible, manually selecting the correct format is recommended.

---

#### Rule-Based Attacks

John supports rule-based password mutations through built-in rule sets.

Rules automatically modify dictionary entries by performing operations such as:

- Capitalization
- Number suffixes
- Symbol insertion

This significantly increases password coverage without performing a full brute-force attack.

---

#### Viewing Cracked Passwords

John stores recovered passwords in its **potfile**.

Previously cracked hashes can be displayed without repeating the attack by using:

```bash
john --show
```

Including the correct hash format ensures previously recovered passwords are displayed correctly.

---

### Hashcat

Hashcat is primarily GPU-accelerated and is significantly faster than CPU-based cracking for many hash algorithms.

It supports:

- Dictionary attacks
- Rule-based attacks
- Mask attacks
- Session management
- GPU acceleration

---

#### Dictionary Attacks

Hashcat dictionary attacks require:

- Hash mode
- Attack mode
- Hash file
- Wordlist

For MD5:

- Mode `0`
- Attack mode `0` (dictionary)

Hashcat rapidly compares candidate passwords against the supplied hashes until matches are found.

---

#### Rule-Based Attacks

Rule files extend a dictionary attack by automatically generating password mutations.

Common rule files include:

- `best64.rule`
- Community rule sets

Rules efficiently test realistic password variations without generating the enormous search space associated with brute force.

---

#### Mask Attacks

Hashcat supports structured brute-force attacks through **mask mode**.

Mask attacks generate only passwords matching a predefined structure.

Example placeholders include:

| Placeholder | Character Set |
|-------------|---------------|
| `?l` | Lowercase letters |
| `?u` | Uppercase letters |
| `?d` | Digits |
| `?s` | Special characters |

Mask attacks are particularly effective when password policies or formats are already known.

---

#### Saving and Viewing Results

Hashcat allows cracked passwords to be:

- Saved to an output file
- Stored in its potfile
- Displayed later using `--show`

Previously recovered hashes do not need to be cracked again, improving efficiency during repeated engagements.

---

#### Session Management

For long-running attacks, Hashcat supports:

- Named sessions
- Interrupted session recovery

This enables password-cracking operations to resume without restarting from the beginning.

---

### John the Ripper vs Hashcat

The lesson compares the strengths of both tools.

| John the Ripper | Hashcat |
|-----------------|----------|
| CPU-oriented | GPU-oriented |
| Excellent format detection | Explicit hash modes |
| Strong support for non-standard formats | Extremely fast for supported algorithms |
| Ideal for quick attempts | Ideal for sustained large-scale attacks |

Neither tool replaces the other.

John excels when dealing with unknown or uncommon formats, while Hashcat is generally preferred for high-speed password cracking.

---

## Skills Practiced

- John the Ripper
- Hashcat
- Dictionary Attacks
- Rule-Based Attacks
- Mask Attacks
- Password Recovery
- Offline Password Cracking

---

## Key Takeaways

- John the Ripper and Hashcat are the two primary offline password-cracking tools used during penetration testing.
- Explicitly specifying the correct hash format or mode improves cracking accuracy.
- Rule-based attacks efficiently expand dictionary coverage using realistic password mutations.
- Hashcat's GPU acceleration makes it significantly faster for many hash algorithms.
- Potfiles and session management allow previously cracked passwords and interrupted attacks to be reused efficiently. :contentReference[oaicite:2]{index=2}