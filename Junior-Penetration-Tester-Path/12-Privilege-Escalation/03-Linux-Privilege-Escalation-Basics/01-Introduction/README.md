# 01-Introduction/README.md

# Introduction

## Overview

The previous room introduced manual Linux enumeration techniques.

This room focuses on **using that information** to escalate privileges by exploiting common Linux misconfigurations such as **sudo**, **SUID**, **PATH hijacking**, **Linux capabilities**, **cron jobs**, and **NFS shares**. Each task targets a different privilege escalation vector and is performed against its own dedicated machine. :contentReference[oaicite:1]{index=1}

---

## Learning Objectives

- Understand common Linux privilege escalation vectors
- Learn manual exploitation techniques
- Apply enumeration findings
- Gain root access

---

## Prerequisites

Before starting this room you should already understand:

- Linux Fundamentals
- Linux Enumeration
- File permissions
- Basic Linux commands

---

## Workflow

```text
Enumerate System
        ↓
Identify Weakness
        ↓
Exploit Misconfiguration
        ↓
Obtain Root
```

---

## Key Takeaways

- Enumeration alone does not provide elevated privileges.
- Exploitation begins once a privilege escalation vector has been identified.
- Each technique demonstrated in this room is based on common real-world Linux misconfigurations. :contentReference[oaicite:2]{index=2}