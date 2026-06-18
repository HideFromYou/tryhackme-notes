# Checkmate (TryHackMe)

## Overview

Checkmate is a password-attacks focused challenge that combines reconnaissance, OSINT, wordlist generation, password cracking concepts, and online brute forcing. The room demonstrates how weak password practices, predictable patterns, and exposed information can be chained together to compromise multiple services.

## Skills Practiced

* Web reconnaissance
* Virtual host configuration
* Password attacks
* Hydra brute forcing
* Custom wordlist generation
* CeWL usage
* OSINT gathering
* Hash identification and cracking
* SHA256 analysis
* SSH password attacks

---

## Enumeration

### Host Discovery

Add discovered virtual hosts:

```bash
echo "TARGET_IP jobs.thm firewall.thm social.thm" >> /etc/hosts
```

Initial scan:

```bash
nmap -sV jobs.thm
```

Discovered services:

```text
22/tcp   SSH
5000/tcp Jobs Portal
5001/tcp FirewallOS
5002/tcp Employee Login
5003/tcp Social Platform
```

---

## Level 1 - Default Credentials

### Objective

Gain access to the FirewallOS portal.

### Methodology

* Inspect login form
* Identify POST endpoint
* Identify username/password fields
* Identify failure response

Example:

```html
<form method="post" action="/login">
```

Hydra was used against the login form with a default credentials wordlist.

Key lesson:

```text
Default credentials remain one of the most common security weaknesses.
```

---

## Level 2 - Company Keyword Passwords

### Objective

Attack the Employee Login panel.

### Methodology

Generate company-specific words from the application.

Example CeWL usage:

```bash
cewl -d 2 -m 6 --lowercase -w keywords.txt http://jobs.thm:5002
```

If CeWL is unavailable:

```bash
curl -s http://jobs.thm:5002 \
| tr '[:upper:]' '[:lower:]' \
| grep -oE '[a-z]{6,}' \
| sort -u > keywords.txt
```

Use generated words as password candidates.

Key lesson:

```text
Target-specific wordlists outperform generic wordlists.
```

---

## Level 3 - OSINT & Personal Information

### Objective

Derive Marco's password using information gathered from the Social platform.

### Methodology

* Review public profile information
* Identify interests
* Identify naming conventions
* Build custom password candidates

Key lesson:

```text
Personal information frequently influences password choices.
```

---

## Level 4 - SHA256 Filename Recovery

### Objective

Recover the original filename of Marco's uploaded profile image.

### Methodology

The application stores files as:

```text
SHA256(original_filename).png
```

Approach:

1. Generate filename candidates
2. Compute SHA256 hashes
3. Compare hashes with the stored image filename

Example:

```bash
echo -n "profile.png" | sha256sum
```

Key lesson:

```text
Predictable filename schemes can expose hidden information.
```

---

## Level 5 - Password Pattern Discovery

### Objective

Compromise Marco's SSH account.

### Methodology

Discover password creation patterns and generate a targeted wordlist.

Useful tools:

```bash
crunch
```

```bash
hydra
```

Example:

```bash
hydra -l marco -P wordlist.txt ssh://TARGET_IP
```

Key lesson:

```text
Predictable password generation rules significantly reduce password strength.
```

---

## Tools Used

### Enumeration

```bash
nmap
curl
ffuf
gobuster
```

### Password Attacks

```bash
hydra
```

### Wordlist Generation

```bash
cewl
crunch
```

### Hash Analysis

```bash
sha256sum
hashcat
john
```

---

## Key Takeaways

* Default credentials remain dangerous.
* Company terminology often becomes passwords.
* OSINT dramatically improves password attacks.
* Custom wordlists outperform generic wordlists.
* Predictable password patterns are easily exploitable.
* Strong password policies must be combined with unique passwords and MFA.
