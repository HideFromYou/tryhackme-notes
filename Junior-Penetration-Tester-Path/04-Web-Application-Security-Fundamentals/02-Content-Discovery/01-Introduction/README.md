# Introduction

## Overview

Content Discovery is a fundamental phase of web application reconnaissance. The objective is to identify hidden files, directories, technologies, and publicly accessible resources before attempting exploitation. Effective content discovery combines manual inspection, OSINT techniques, and automated enumeration tools to build a complete understanding of the target application.

---

## Learning Objectives

- Understand the purpose of content discovery
- Learn different reconnaissance techniques
- Identify publicly accessible resources
- Discover hidden application content
- Build an effective web reconnaissance workflow

---

## What is Content Discovery?

Content Discovery is the process of locating resources that are available on a web server but may not be directly linked from the application's interface.

Examples include:

- Hidden directories
- Backup files
- Configuration files
- Login portals
- Development pages
- Administrative interfaces
- API endpoints

Finding these resources expands the application's attack surface and provides valuable information for later testing.

---

## Discovery Approaches

Successful reconnaissance combines multiple techniques rather than relying on a single method.

### Manual Discovery

Inspect the application using a web browser to identify:

- Public pages
- robots.txt
- sitemap.xml
- HTTP headers
- Page source
- Developer tools

---

### Open-Source Intelligence (OSINT)

Gather publicly available information using external resources such as:

- Search engines
- Technology fingerprinting tools
- Internet archives
- Public code repositories
- Cloud storage services

---

### Automated Discovery

Use specialised tools to enumerate:

- Directories
- Files
- Subdomains
- Virtual hosts

Automation increases coverage and helps identify resources that may be missed during manual analysis.

---

## Why Content Discovery Matters

Hidden resources often expose valuable information including:

- Sensitive files
- Administrative functionality
- Development environments
- Internal documentation
- Misconfigured services

A thorough discovery process significantly improves the effectiveness of later penetration testing activities.

---

## Skills Practiced

- Web reconnaissance
- Information gathering
- Attack surface mapping
- Manual enumeration
- Automated enumeration
- OSINT research

---

## Key Takeaways

- Content discovery is a critical reconnaissance phase.
- Combine manual, OSINT, and automated techniques.
- Hidden resources frequently expose valuable information.
- A complete attack surface improves penetration testing efficiency.
- Reconnaissance should always precede exploitation.