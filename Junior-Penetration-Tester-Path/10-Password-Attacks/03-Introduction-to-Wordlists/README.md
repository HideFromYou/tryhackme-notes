# Introduction to Wordlists

## Overview

Wordlists are one of the most fundamental resources used during penetration testing and offensive security. They provide collections of potential usernames, passwords, directory names, subdomains, and other strings that can be supplied to automated tools for password attacks, enumeration, fuzzing, and vulnerability discovery.

This module teaches how to build, refine, and effectively use both public and custom wordlists. Instead of relying solely on generic password lists, penetration testers learn how to gather target-specific information using **Open Source Intelligence (OSINT)**, generate tailored wordlists, clean them for efficiency, and use them with common offensive security tools. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this module, you should be able to:

- Understand what wordlists are and where they are used
- Gather target-specific information using OSINT
- Build and clean custom wordlists
- Generate targeted password lists
- Use wordlists with enumeration and brute-force tools
- Improve the effectiveness of password attacks through customized wordlists

---

# Module Structure

## 01. Introduction

Introduces wordlists, explains their role in penetration testing, and outlines the objectives of the module.

Topics include:

- Wordlist fundamentals
- Offensive security applications
- OSINT overview
- Prerequisites

---

## 02. Wordlists

Explains what wordlists are, where they are used, and introduces common public and custom wordlist sources.

Topics include:

- Password wordlists
- Directory enumeration
- Service brute forcing
- Common tools
- SecLists
- RockYou
- Crunch

---

## 03. Gathering Information for Custom Wordlists

Focuses on collecting target-specific information using Open Source Intelligence (OSINT).

Topics include:

- Website analysis
- Public documents
- Company information
- Employee names
- Username generation
- Target profiling

---

## 04. Creating and Cleaning Wordlists

Demonstrates how to merge, normalize, filter, and optimize raw wordlists for practical use.

Topics include:

- Deduplication
- Lowercasing
- Filtering
- Username generation
- Pattern-based password generation
- Crunch

---

## 05. Using Your Wordlist

Shows how customized wordlists are used with common penetration testing tools.

Topics include:

- ffuf
- Directory discovery
- Hydra
- Login brute forcing
- Enumeration workflow

---

## 06. Conclusion

Summarizes the complete workflow from OSINT gathering to building, cleaning, and using custom wordlists during penetration tests.

---

## Skills Practiced

- Wordlist Creation
- OSINT
- Password Attacks
- Directory Enumeration
- Username Generation
- Fuzzing
- Brute Force
- Penetration Testing

---

## Tools & Technologies

- Hydra
- ffuf
- Crunch
- SecLists
- RockYou
- Linux
- HTTP
- OSINT

---

## Prerequisites

Before studying this module, you should be familiar with:

- Linux Command Line
- HTTP Fundamentals
- Authentication Concepts
- Basic Networking
- Web Applications

---

## Key Takeaways

- Wordlists are essential for password attacks, enumeration, and fuzzing.
- Target-specific wordlists are significantly more effective than generic lists.
- OSINT provides valuable information for building customized wordlists.
- Cleaning and optimizing wordlists improves both efficiency and accuracy.
- Combining customized wordlists with tools such as Hydra and ffuf greatly increases the effectiveness of penetration testing engagements. 