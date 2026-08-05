# Hydra

## Overview

Hydra is one of the most widely used **online password brute-force** tools in penetration testing. It automates authentication attempts against network services by testing usernames and passwords from supplied wordlists, allowing penetration testers to evaluate the strength of authentication mechanisms and identify weak credentials.

Unlike offline password cracking tools, Hydra communicates directly with live services such as SSH, FTP, HTTP forms, SMB, RDP, and many others. Because it performs authentication attempts against running services, Hydra should only be used during authorized security assessments.

---

## Learning Objectives

After completing this module, you should be able to:

- Understand what Hydra is
- Explain how online password attacks work
- Identify services supported by Hydra
- Perform brute-force attacks against authentication services
- Understand password security best practices
- Use Hydra responsibly during penetration tests

---

# Module Structure

## 01. Hydra Introduction

Introduces Hydra, explains how online password brute forcing works, and discusses the importance of strong passwords.

Topics include:

- What Hydra is
- Online brute-force attacks
- Supported protocols
- Password security
- Default credentials

---

## 02. Using Hydra

Demonstrates how to use Hydra against various authentication services.

Topics include:

- Hydra syntax
- Username and password lists
- SSH brute forcing
- HTTP form attacks
- FTP authentication
- Practical attack examples

---

## 03. Conclusion

Summarizes Hydra's capabilities, responsible usage, and defensive recommendations for protecting authentication services.

---

## Skills Practiced

- Online Password Attacks
- Brute Force
- Authentication Testing
- Password Security
- Penetration Testing
- Credential Auditing

---

## Tools & Technologies

- Hydra
- SSH
- FTP
- HTTP Forms
- SMB
- RDP
- Wordlists
- Linux

---

## Prerequisites

Before studying this module, you should be familiar with:

- Linux Fundamentals
- Command Line Usage
- Authentication Concepts
- Basic Networking
- Password Security

---

## Key Takeaways

- Hydra is an online password brute-force tool used to test authentication services.
- It supports numerous protocols, including SSH, FTP, HTTP, SMB, RDP, and many others.
- Weak or default passwords can often be discovered quickly using common password lists.
- Strong password policies and multi-factor authentication significantly reduce brute-force risks.
- Hydra should only be used during authorized penetration tests and security assessments.