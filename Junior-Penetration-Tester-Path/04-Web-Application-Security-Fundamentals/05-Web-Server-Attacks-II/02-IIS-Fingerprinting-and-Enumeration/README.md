# IIS Fingerprinting and Enumeration

## Overview

Fingerprinting IIS allows analysts to determine the server version, supported features, authentication methods, and available functionality before attempting any security testing.

Accurate enumeration provides valuable context for identifying configuration weaknesses and version-specific vulnerabilities.

---

## Learning Objectives

- Understand IIS fingerprinting
- Identify Microsoft IIS deployments
- Learn common enumeration techniques
- Recognise IIS-specific response characteristics
- Understand the value of version identification

---

## Identifying IIS

Common indicators include:

- `Server: Microsoft-IIS`
- ASP.NET response headers
- Windows authentication prompts
- Default IIS error pages
- Characteristic HTTP responses

Combining multiple observations increases fingerprinting confidence.

---

## HTTP Enumeration

Useful information can be collected by examining:

- Response headers
- Supported HTTP methods
- Authentication challenges
- Redirect behaviour
- Response codes

These responses reveal valuable details about the web server configuration.

---

## Authentication

IIS commonly supports several authentication mechanisms, including:

- Anonymous Authentication
- Basic Authentication
- Windows Authentication
- NTLM
- Integrated Windows Authentication

Understanding the active authentication method helps guide further assessment.

---

## Version Identification

Determining the IIS version assists analysts by allowing them to:

- Research known vulnerabilities
- Identify supported features
- Understand default configurations
- Prioritise testing activities

---

## Skills Practiced

- IIS fingerprinting
- HTTP enumeration
- Version identification
- Authentication analysis
- Passive reconnaissance

---

## Key Takeaways

- IIS exposes several identifiable characteristics.
- Authentication mechanisms provide valuable reconnaissance data.
- Version information supports targeted vulnerability research.
- Enumeration should always precede active testing.
- Multiple indicators improve identification accuracy.