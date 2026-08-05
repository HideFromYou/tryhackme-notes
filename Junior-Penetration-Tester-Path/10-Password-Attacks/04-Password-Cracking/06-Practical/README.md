# Practical

## Overview

This practical exercise brings together the concepts covered throughout the module by applying the complete **offline password-cracking workflow** against several password hashes. Rather than focusing on individual commands, the exercise emphasizes the decision-making process followed during a real penetration test: identify the hash, select the correct cracking mode, choose an appropriate attack strategy, and recover the plaintext password.

The lab reinforces the importance of identifying hash algorithms correctly before attempting to crack them and demonstrates how different algorithms require different tools and configurations. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify unknown password hashes
- Select the correct Hashcat mode or John the Ripper format
- Perform dictionary attacks against multiple hash types
- Recover plaintext passwords from offline hashes
- Apply a structured password-cracking workflow
- Understand how different hashing algorithms affect cracking speed

---

## Main Content

### Practical Workflow

The practical consists of four hash files that should be processed sequentially.

For each hash, the recommended workflow is:

1. Identify the hashing algorithm.
2. Verify the result using hash identification tools.
3. Select the correct Hashcat mode or John format.
4. Perform a dictionary attack using the RockYou wordlist.
5. Recover the plaintext password if a match is found.

This structured methodology mirrors the workflow used during real penetration testing engagements. :contentReference[oaicite:1]{index=1}

---

### Step 1 – Identify the Hash

Before launching any attack, each hash should be analyzed using tools such as:

- `hashid`
- `hashcat --identify`

Correct identification ensures the appropriate cracking mode is selected.

Using the wrong algorithm will cause the attack to fail even if the password exists in the supplied wordlist.

---

### Step 2 – Select the Correct Cracking Mode

Once the algorithm has been identified, the corresponding:

- Hashcat mode
- John the Ripper format

must be selected.

Correct configuration is essential for successful password recovery.

---

### Step 3 – Dictionary Attack

The exercise uses the standard **RockYou** password dictionary:

```text
/usr/share/wordlists/rockyou.txt
```

Each hash is tested against this wordlist to determine whether the original password appears in a known password collection.

---

### Different Algorithms, Same Password

An important observation from the exercise is that two hashes may contain the **same plaintext password** while producing completely different hash values.

This demonstrates that:

- The hashing algorithm determines the output.
- Identical passwords hashed with different algorithms produce different hashes.
- Correct algorithm identification is just as important as selecting the appropriate attack.

---

### bcrypt Performance

The final exercise uses **bcrypt**.

Unlike fast algorithms such as MD5, bcrypt intentionally requires significantly more computation for every password guess.

As a result:

- Dictionary attacks take noticeably longer.
- Brute-force attacks become considerably more expensive.
- Password storage is significantly more resistant to offline attacks.

This behavior is an intentional security feature rather than a performance limitation.

---

## Skills Practiced

- Hash Identification
- Dictionary Attacks
- Hashcat
- John the Ripper
- Password Recovery
- Offline Password Cracking
- Penetration Testing

---

## Key Takeaways

- Successful password cracking follows a structured workflow rather than random tool usage.
- Correctly identifying the hash algorithm is the first and most important step.
- Dictionary attacks remain the preferred first approach for offline password cracking.
- Identical passwords produce different hashes when different algorithms are used.
- Modern password hashing algorithms such as bcrypt intentionally slow password verification, making offline password cracking significantly more difficult. :contentReference[oaicite:2]{index=2}