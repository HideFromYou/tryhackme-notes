# Common Misconfigurations Across Servers

## Overview

Although web servers differ in architecture and configuration, many security issues arise from the same underlying problem: insecure default settings or incomplete hardening. Recognising these common misconfigurations helps security professionals identify weaknesses regardless of the server technology in use.

---

## Learning Objectives

- Identify common web server misconfigurations
- Understand how default settings create security risks
- Recognise information disclosure issues
- Learn general server hardening principles
- Compare security concerns across different web servers

---

## Common Misconfigurations

Several configuration issues appear across multiple web server platforms.

Examples include:

- Version disclosure
- Directory listing
- Exposed status pages
- Missing security headers
- Weak default configurations
- Unnecessary services

These issues often reveal valuable information during reconnaissance.

---

## Information Disclosure

Servers frequently expose technical details that assist attackers during the reconnaissance phase.

Examples include:

- Software names
- Version numbers
- Internal paths
- Error messages
- Debug information
- Environment details

Reducing unnecessary information disclosure limits intelligence available to attackers.

---

## Directory Listings

Directory indexing can unintentionally expose:

- Source code
- Configuration files
- Backups
- Uploaded content
- Documentation

Unless intentionally required, directory listings should be disabled on production systems.

---

## Security Headers

HTTP security headers help browsers enforce additional security protections.

Common headers include:

- Content-Security-Policy
- X-Frame-Options
- X-Content-Type-Options
- Referrer-Policy
- Strict-Transport-Security

Missing headers do not always indicate a vulnerability but may weaken overall security.

---

## Administrative Interfaces

Status pages and administrative endpoints should only be accessible to authorised users.

Public exposure may reveal:

- Server statistics
- Performance information
- Internal configuration
- Operational details

Proper access control is essential.

---

## Hardening Best Practices

A secure deployment should aim to:

- Remove unnecessary information disclosure
- Disable unused features
- Restrict administrative interfaces
- Configure security headers
- Keep software updated
- Review default configurations

---

## Skills Practiced

- Security assessment
- Configuration review
- Information disclosure analysis
- HTTP header inspection
- Web server hardening

---

## Key Takeaways

- Many web server vulnerabilities originate from insecure configurations.
- Similar security issues appear across different server platforms.
- Information disclosure should be minimised.
- Proper hardening significantly improves security.
- Configuration reviews are an essential part of web assessments.