# Wordlists and Attack Strategies

## Overview

Once the hash type has been identified, the next step is choosing the most effective password-cracking strategy. No single attack method works in every situation. Successful password cracking depends on selecting the right approach based on the available information about the target, the password policy, and the expected password complexity.

This lesson introduces the four primary password-cracking strategies: **dictionary attacks**, **brute-force attacks**, **rule-based attacks**, and **mask attacks**, explaining when each should be used and their advantages and limitations. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand common password-cracking strategies
- Differentiate between dictionary, brute-force, rule-based, and mask attacks
- Select the appropriate attack for different scenarios
- Understand the importance of high-quality wordlists
- Apply password mutation techniques
- Recognize when custom wordlists provide an advantage

---

## Main Content

### Choosing the Right Strategy

Password cracking is not simply about trying every possible password.

A penetration tester should first evaluate:

- Available information about the target
- Password policies
- Expected password patterns
- Time and computational resources

Selecting the wrong attack wastes both time and computing power.

---

### Dictionary Attacks

A **dictionary attack** tests passwords from a predefined wordlist.

Rather than generating random combinations, it checks passwords that people have actually used.

Common wordlists include:

- `rockyou.txt`
- SecLists password collections

Because these lists are based on real-world password leaks, they remain one of the fastest and most effective first attacks.

However, dictionary attacks only succeed if the password exists exactly as written within the wordlist. :contentReference[oaicite:1]{index=1}

---

### Brute-Force Attacks

A **brute-force attack** generates every possible password combination within a defined character set and length.

Unlike dictionary attacks, brute force eventually finds the correct password if enough time is available.

However, the search space grows exponentially as password length and complexity increase.

Brute force is therefore most practical for:

- Short passwords
- PIN codes
- Small search spaces

Long, complex passwords quickly become computationally impractical.

---

### Rule-Based Attacks

Rule-based attacks improve dictionary attacks by automatically modifying existing words.

Common mutations include:

- Capitalizing letters
- Appending numbers
- Adding special characters
- Replacing letters with symbols

Examples:

- `password` → `Password`
- `password` → `password1`
- `password` → `password!`
- `password` → `p@ssw0rd`

These transformations reflect common password habits while avoiding the enormous search space of full brute-force attacks.

Popular Hashcat rule files include:

- `best64.rule`
- `rockyou-30000.rule`
- `d3ad0ne.rule`
- `dive.rule`

John the Ripper also provides built-in rule sets for password mutations. :contentReference[oaicite:2]{index=2}

---

### Mask Attacks

A **mask attack** is a structured brute-force attack that generates passwords matching a known pattern.

Instead of searching every possible combination, the attacker specifies the expected password structure.

Hashcat placeholders include:

| Placeholder | Character Set |
|-------------|---------------|
| `?l` | Lowercase letters |
| `?u` | Uppercase letters |
| `?d` | Digits |
| `?s` | Special characters |
| `?a` | All printable ASCII |

When password policies are known, mask attacks dramatically reduce the search space while remaining highly effective.

---

### Selecting the Appropriate Attack

The lesson provides general recommendations for choosing an attack strategy.

| Scenario | Recommended Attack |
|----------|--------------------|
| No password information | Dictionary attack |
| Dictionary attack fails | Dictionary + Rules |
| Known password pattern | Mask attack |
| Very short password | Brute-force attack |
| Company-specific passwords | Custom wordlist + Rules |

Beginning with the least expensive attack and gradually increasing complexity provides the most efficient workflow.

---

## Skills Practiced

- Dictionary Attacks
- Brute-Force Attacks
- Rule-Based Attacks
- Mask Attacks
- Password Analysis
- Wordlists
- Password Cracking

---

## Key Takeaways

- Dictionary attacks should generally be the first password-cracking technique attempted.
- Brute-force attacks guarantee coverage but become impractical as password complexity increases.
- Rule-based attacks efficiently expand dictionary coverage using realistic password mutations.
- Mask attacks are highly effective when password structures or policies are known.
- Choosing the correct attack strategy significantly improves password-cracking efficiency while reducing unnecessary computation. :contentReference[oaicite:3]{index=3}