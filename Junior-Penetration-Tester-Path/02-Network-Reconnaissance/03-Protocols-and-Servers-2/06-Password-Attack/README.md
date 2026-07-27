# Password Attack

## Overview

Password attacks attempt to gain unauthorized access by guessing, reusing, or brute-forcing user credentials.

## Learning Objectives

- Understand password attack techniques
- Learn common password attack tools
- Identify effective mitigations

## Common Attack Types

- Password Guessing
- Dictionary Attack
- Brute Force
- Credential Stuffing
- Password Spraying
- Hybrid Attack

## Common Tools

- Hydra
- Hashcat
- John the Ripper
- Medusa
- Ncrack

## Example

```bash
hydra -l username -P rockyou.txt <TARGET_IP> ssh
```

## Skills Practiced

- Authentication Testing
- Password Auditing
- Service Enumeration

## Key Takeaways

- Weak or reused passwords are easily compromised.
- Multi-Factor Authentication (MFA) significantly improves security.
- Rate limiting and account lockouts reduce brute-force attacks.