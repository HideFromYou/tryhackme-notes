# Automated Discovery - Gobuster Fundamentals

## Overview

Manual reconnaissance and OSINT provide valuable information, but automated discovery significantly expands coverage. Gobuster is a popular enumeration tool used to discover hidden directories and files by testing large wordlists against a target web server.

---

## Learning Objectives

- Understand automated content discovery
- Learn the purpose of Gobuster
- Explore directory enumeration
- Understand the role of wordlists
- Interpret enumeration results

---

## What is Gobuster?

Gobuster is an open-source enumeration tool written in Go.

It supports multiple discovery modes, including:

- Directory enumeration
- File discovery
- DNS subdomain enumeration
- Virtual host enumeration

Its speed and flexibility make it a common tool during web reconnaissance.

---

## Directory Enumeration

Directory enumeration attempts to discover hidden resources by requesting common directory and file names.

Typical discoveries include:

- Administrative panels
- Backup files
- Development directories
- Configuration files
- Login pages
- Public documents

Enumeration helps map the application's structure beyond visible navigation.

---

## Wordlists

Gobuster relies on wordlists that contain commonly used names for directories and files.

Good wordlists improve the effectiveness of discovery by covering frequently used naming conventions.

Selecting an appropriate wordlist depends on the target application and the desired level of coverage.

---

## Understanding Results

Enumeration results commonly include:

- Accessible directories
- Existing files
- Redirects
- HTTP status codes
- Response sizes

Analysing these responses helps determine which resources deserve further investigation.

---

## Performance Considerations

Enumeration tools generate many requests in a short period.

Important considerations include:

- Thread count
- Request delays
- Response filtering
- Output logging

Balancing speed and accuracy produces more reliable results.

---

## Skills Practiced

- Automated reconnaissance
- Directory enumeration
- File discovery
- Wordlist usage
- Result analysis

---

## Key Takeaways

- Gobuster automates web content discovery.
- Wordlists are essential for effective enumeration.
- Hidden resources expand the application's attack surface.
- Response analysis helps prioritise findings.
- Automated discovery complements manual reconnaissance.