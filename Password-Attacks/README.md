Password-Attacks/
├── README.md
├── Phishing.md
├── Hydra.md
├── Wordlists.md
├── Password-Cracking.md
└── Checkmate.md

# Password Attacks

## Overview

This path covers password attacks, credential harvesting, wordlist generation, brute forcing, hash identification, and password cracking techniques used during penetration testing.

---

# Rooms Completed

- Phishing
- Hydra
- Wordlists
- Password Cracking
- Checkmate (Capstone)

---

# Phishing

## Key Concepts

- Social Engineering
- Credential Harvesting
- Email Spoofing
- Typosquatting
- Spear Phishing
- Whaling

## Social Engineering Principles

- Scarcity
- Urgency
- Authority
- Fear
- Curiosity
- Trust

## Tools

### Social Engineering Toolkit (SET)

```bash
SET
```

### Credential Harvester Workflow

```text
Social Engineering Attacks
→ Website Attack Vectors
→ Credential Harvester
→ Custom Import
```

## Lessons Learned

- Humans are often the weakest security control.
- Internal-looking emails are highly effective.
- Typosquatted domains increase success rates.

---

# Hydra

## Purpose

Online password brute forcing.

## Common Protocols

- SSH
- FTP
- HTTP
- HTTPS
- SMB
- RDP
- SMTP
- LDAP

## SSH Brute Force

```bash
hydra -l user -P passwords.txt TARGET_IP ssh
```

## HTTP POST Login

```bash
hydra -l user \
-P passwords.txt \
TARGET_IP \
http-post-form \
"/:username=^USER^&password=^PASS^:F=incorrect"
```

## Lessons Learned

- Weak passwords are quickly discovered.
- Always verify login request parameters before attacking.

---

# Wordlists

## Sources

### RockYou

```bash
/usr/share/wordlists/rockyou.txt
```

### SecLists

```bash
/usr/share/wordlists/SecLists
```

## Custom Wordlists

### CeWL

```bash
cewl -d 2 -m 3 \
--lowercase \
-e \
--email_file emails.txt \
-w words.txt \
http://target
```

### Crunch

```bash
crunch 11 11 -t Helios20%%!
```

## Username Generation

Common formats:

```text
first.last
flast
firstl
```

## Lessons Learned

- Custom wordlists outperform generic wordlists.
- OSINT dramatically improves success rates.

---

# Password Cracking

## Password Storage

Passwords should be stored as:

```text
hash(password + salt)
```

Never plaintext.

## Hashing Algorithms

| Algorithm | Status |
|------------|---------|
| MD5 | Deprecated |
| SHA1 | Deprecated |
| SHA256 | Weak for passwords |
| NTLM | Legacy |
| bcrypt | Recommended |
| Argon2 | Recommended |

---

## Hash Identification

### hashid

```bash
hashid HASH
```

### Hashcat

```bash
hashcat --identify HASH
```

---

## Common Hashcat Modes

| Algorithm | Mode |
|------------|------|
| MD5 | 0 |
| SHA1 | 100 |
| SHA256 | 1400 |
| SHA512 | 1700 |
| NTLM | 1000 |
| bcrypt | 3200 |

---

## Dictionary Attack

### Hashcat

```bash
hashcat -m 0 -a 0 hash.txt rockyou.txt
```

### John the Ripper

```bash
john --format=raw-md5 \
--wordlist=rockyou.txt \
hash.txt
```

---

## Rule-Based Attack

```bash
hashcat -r best64.rule
```

```bash
john --rules=wordlist
```

---

## Mask Attack

```bash
hashcat -a 3
```

Examples:

```text
?u?l?l?l?l?l?d?d?d?d?s
```

## Lessons Learned

- Identify the hash before cracking.
- Dictionary → Rules → Mask is the standard workflow.
- bcrypt is intentionally slow.

---

# Checkmate (Capstone)

## Objectives

Combine:

- OSINT
- Username Enumeration
- Custom Wordlists
- Hydra
- Hashcat
- John the Ripper

## Methodology

### Recon

- Employees
- Emails
- Technologies
- Public Information

### Wordlist Generation

- CeWL
- Crunch
- SecLists

### Password Attacks

- Online (Hydra)
- Offline (Hashcat / John)

### Compromise

Reuse credentials across services.

## Lessons Learned

- Password reuse remains common.
- OSINT provides valuable attack surface information.
- Custom wordlists significantly improve attack success rates.

---

# Key Takeaways

- Social engineering remains highly effective.
- Weak passwords fail quickly.
- Custom wordlists outperform generic lists.
- Proper hash identification is critical.
- bcrypt and Argon2 are the preferred password storage algorithms.
- Password attacks become significantly more effective when combined with OSINT.
