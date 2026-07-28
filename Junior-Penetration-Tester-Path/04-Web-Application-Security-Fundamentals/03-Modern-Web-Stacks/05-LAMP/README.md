# LAMP

## Overview

The LAMP stack is one of the oldest and most widely deployed web application platforms. It combines Linux, Apache, MySQL, and PHP to deliver dynamic web applications and remains common in enterprise environments, legacy systems, and content management platforms.

Understanding how to identify LAMP environments allows penetration testers to recognise common technologies and investigate framework-specific vulnerabilities.

---

## Learning Objectives

- Understand the components of the LAMP stack
- Identify Apache web servers
- Learn common fingerprinting indicators
- Recognise version disclosure
- Understand why server identification matters

---

## What is the LAMP Stack?

LAMP is composed of four core technologies:

- Linux
- Apache HTTP Server
- MySQL
- PHP

Each component provides part of the infrastructure required to host dynamic web applications.

---

## Apache HTTP Server

Apache is responsible for:

- Serving web content
- Processing HTTP requests
- Managing virtual hosts
- Supporting modules
- Delivering static and dynamic resources

Because Apache is highly configurable, understanding its behaviour is important during reconnaissance.

---

## Fingerprinting Apache

Common indicators include:

- `Server` response header
- Default error pages
- HTTP response behaviour
- Supported HTTP methods
- Default Apache resources

Version information exposed through headers can greatly simplify vulnerability research.

---

## Version Identification

Knowing the exact software version allows analysts to:

- Search for known CVEs
- Review security advisories
- Determine patch status
- Prioritise testing efforts

Version disclosure is one of the most valuable findings during reconnaissance.

---

## Security Considerations

During fingerprinting, analysts should review:

- Server headers
- Enabled HTTP methods
- Security headers
- Directory indexing
- Default configuration behaviour

These observations help identify potential weaknesses before exploitation.

---

## Skills Practiced

- Apache fingerprinting
- Server identification
- HTTP analysis
- Version research
- Passive reconnaissance

---

## Key Takeaways

- LAMP remains one of the most common web application stacks.
- Apache often exposes valuable fingerprinting information.
- Version identification supports targeted vulnerability research.
- Server configuration influences the application's security posture.
- Passive reconnaissance provides the foundation for informed testing.