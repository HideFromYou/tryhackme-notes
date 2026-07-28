# Automation

## Overview

Manual enumeration provides valuable insight into how IIS behaves, but automated tools can quickly collect the same information across multiple targets. Automation allows security professionals to identify common IIS features, supported HTTP methods, authentication mechanisms, and exposed services in a consistent and repeatable manner.

This lesson focuses on using automated reconnaissance to complement manual analysis rather than replace it.

---

## Learning Objectives

- Understand automated IIS reconnaissance
- Learn the purpose of Nmap NSE scripts
- Identify WebDAV automatically
- Enumerate HTTP methods
- Compare manual and automated enumeration

---

## Nmap Scripting Engine (NSE)

The Nmap Scripting Engine (NSE) extends Nmap beyond port scanning by providing scripts that perform application-specific enumeration.

For IIS assessments, NSE can help identify:

- Supported HTTP methods
- WebDAV functionality
- Authentication mechanisms
- Server information
- Service versions

Automation allows these checks to be performed in a single workflow.

---

## Service Detection

Version detection provides valuable information before vulnerability research begins.

Typical information gathered includes:

- Web server software
- Version numbers
- Operating system hints
- Available services

Accurate version identification helps prioritise later security testing.

---

## Automated Enumeration

Automation can identify:

- Allowed HTTP methods
- WebDAV support
- Authentication challenges
- Server capabilities
- Configuration details

The collected information should always be validated through manual analysis when necessary.

---

## Benefits of Automation

Automated reconnaissance offers several advantages:

- Faster assessments
- Consistent results
- Broad coverage
- Reduced manual effort
- Efficient large-scale scanning

However, automation should support—not replace—manual investigation.

---

## Best Practices

A recommended workflow includes:

1. Identify the server.
2. Perform automated enumeration.
3. Validate important findings manually.
4. Investigate exposed functionality.
5. Continue with targeted testing.

---

## Skills Practiced

- Automated reconnaissance
- Nmap NSE usage
- IIS enumeration
- Service detection
- Security assessment workflow

---

## Key Takeaways

- Automation improves efficiency during reconnaissance.
- Nmap NSE scripts simplify IIS enumeration.
- Version detection guides vulnerability research.
- Manual validation remains essential.
- Combining automated and manual techniques produces the best results.