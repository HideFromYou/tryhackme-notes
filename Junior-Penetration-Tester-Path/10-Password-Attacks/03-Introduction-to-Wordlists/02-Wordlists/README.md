# Wordlists

## Overview

A **wordlist** is a text file where each line contains a potential password, username, filename, directory name, subdomain, or other string used during automated security testing. Rather than manually guessing values, penetration testing tools read entries from a wordlist and systematically test each one against a target.

Wordlists are essential throughout offensive security, supporting password attacks, login brute forcing, directory enumeration, subdomain discovery, and web fuzzing. Their effectiveness depends not only on their size but also on how well they match the target being assessed. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what a wordlist is
- Explain where wordlists are used
- Identify common tools that rely on wordlists
- Differentiate between pre-made and custom wordlists
- Understand when automated wordlist generation is useful

---

## Main Content

### What is a Wordlist?

A wordlist is a plain text file where every line contains a possible value that security tools can automatically test.

Wordlists may contain:

- Passwords
- Usernames
- Directory names
- File names
- Subdomains
- API endpoints

Instead of manually testing each value, offensive security tools process every entry automatically. :contentReference[oaicite:1]{index=1}

---

### Where Are Wordlists Used?

Wordlists support many penetration testing activities.

Common use cases include:

- Password guessing and cracking
- Service login brute forcing
- Directory and file enumeration
- Subdomain discovery
- Web application fuzzing

Because many attacks depend on testing large numbers of potential values, wordlists are fundamental to automated security assessments. :contentReference[oaicite:2]{index=2}

---

### Common Tools That Use Wordlists

Several penetration testing tools rely heavily on wordlists.

| Tool | Primary Use |
|------|-------------|
| **John the Ripper** | Password cracking |
| **Hashcat** | Password cracking |
| **Hydra** | Online login brute forcing |
| **Gobuster** | Directory enumeration |
| **ffuf** | Directory, parameter, and subdomain fuzzing |
| **Burp Suite** | Web fuzzing |
| **OWASP ZAP** | Web fuzzing |
| **Aircrack-ng** | Wireless password cracking | :contentReference[oaicite:3]{index=3}

---

### Sources of Wordlists

Wordlists generally come from three sources.

#### Pre-made Wordlists

Public collections provide broad coverage for common attacks.

Popular examples include:

- **rockyou.txt**
- **SecLists**

These collections contain passwords, usernames, directories, subdomains, API endpoints, and many other useful lists. :contentReference[oaicite:4]{index=4}

---

#### Custom Wordlists

Custom wordlists are built specifically for the target.

They may include:

- Employee names
- Company terminology
- Local language
- Industry-specific words
- Cultural references

Targeted lists are often more efficient than large generic wordlists because they better reflect the organization's environment. :contentReference[oaicite:5]{index=5}

---

#### Automated Wordlist Generation

Sometimes password patterns are known.

In these situations, generators such as **Crunch** create every possible combination matching a specified pattern.

Example use cases include:

- Fixed password formats
- PIN generation
- Character combination testing

Generated lists can also be piped directly into other penetration testing tools. :contentReference[oaicite:6]{index=6}

---

## Skills Practiced

- Wordlists
- Password Attacks
- Directory Enumeration
- Web Fuzzing
- OSINT
- Penetration Testing

---

## Key Takeaways

- Wordlists are text files containing values used during automated security testing.
- They are used for password attacks, enumeration, fuzzing, and resource discovery.
- Popular tools such as Hydra, Hashcat, John the Ripper, Gobuster, and ffuf all rely on wordlists.
- Pre-made collections like RockYou and SecLists provide broad coverage, while custom wordlists improve efficiency by targeting specific organizations.
- Automated generators such as Crunch are useful when password patterns are known. :contentReference[oaicite:7]{index=7}