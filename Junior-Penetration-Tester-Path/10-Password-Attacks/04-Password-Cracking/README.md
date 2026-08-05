# Password Cracking

## Overview

Password cracking is a fundamental skill in penetration testing and red team operations. When password hashes are obtained from leaked databases, compromised systems, or captured authentication data, the next objective is to recover the original plaintext passwords.

This module introduces the complete password cracking workflow, from understanding how passwords are stored to identifying hash types, selecting appropriate attack strategies, and using industry-standard tools such as **John the Ripper** and **Hashcat**. It concludes with a practical exercise that combines these techniques in a realistic penetration testing scenario. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this module, you should be able to:

- Understand how passwords are stored securely
- Identify common password hash formats
- Select appropriate password-cracking strategies
- Use wordlists effectively
- Perform offline password cracking with John the Ripper
- Perform offline password cracking with Hashcat
- Choose the appropriate attack technique for different scenarios

---

# Module Structure

## 01. Introduction

Introduces password cracking fundamentals, explains the learning objectives, and outlines the workflow used throughout the module.

Topics include:

- Password cracking overview
- Hashes
- Attack workflow
- Learning objectives

---

## 02. How Passwords Are Stored

Explains how modern systems store passwords securely using cryptographic hash functions.

Topics include:

- Hashing
- Salting
- Password storage
- Secure password practices

---

## 03. Identifying Hash Types

Demonstrates how to recognize common hash formats and use tools to identify unknown hashes.

Topics include:

- Hash identification
- Hash visual characteristics
- hashid
- Hashcat identification
- Selecting the correct hash mode

---

## 04. Wordlists and Attack Strategies

Introduces common password-cracking strategies and explains when each should be used.

Topics include:

- Dictionary attacks
- Rule-based attacks
- Mask attacks
- Brute-force attacks
- Attack selection

---

## 05. Cracking with John the Ripper and Hashcat

Demonstrates practical password cracking using two of the industry's most popular offline cracking tools.

Topics include:

- John the Ripper
- Hashcat
- Dictionary attacks
- Rule-based attacks
- Mask attacks
- Potfiles
- Session management

---

## 06. Practical

Applies the complete password-cracking workflow against multiple password hashes.

Topics include:

- Hash identification
- Tool selection
- Dictionary attacks
- Password recovery
- Practical workflow

---

## 07. Conclusion

Summarizes the password-cracking process and reinforces both offensive and defensive best practices.

---

## Skills Practiced

- Password Cracking
- Hash Identification
- Dictionary Attacks
- Rule-Based Attacks
- Mask Attacks
- John the Ripper
- Hashcat
- Offline Password Auditing

---

## Tools & Technologies

- John the Ripper
- Hashcat
- hashid
- RockYou
- SecLists
- Linux
- Wordlists

---

## Prerequisites

Before studying this module, you should be familiar with:

- Linux Fundamentals
- Hashing Basics
- Wordlists
- Basic Command Line
- Authentication Concepts

---

## Key Takeaways

- Password cracking follows a structured workflow beginning with hash identification.
- Selecting the correct attack strategy is as important as selecting the correct tool.
- Dictionary attacks should generally be attempted before more expensive attack methods.
- John the Ripper and Hashcat each have strengths depending on the hash format and cracking scenario.
- Strong password hashing algorithms, salting, and modern password policies significantly increase resistance against offline password-cracking attacks. 