# Introduction

## Overview

Microsoft Internet Information Services (IIS) is one of the most widely deployed web servers in Windows environments. It supports technologies such as ASP.NET, WebDAV, and various authentication mechanisms, making it a common target during enterprise penetration tests.

This room introduces IIS reconnaissance techniques, common misconfigurations, and Windows-specific attack surfaces that can be identified through careful enumeration.

---

## Learning Objectives

- Understand the role of IIS in Windows environments
- Learn how to fingerprint IIS servers
- Identify IIS-specific features
- Recognise common attack surfaces
- Build a structured IIS assessment methodology

---

## What is IIS?

Internet Information Services (IIS) is Microsoft's web server platform used to host:

- Websites
- Web applications
- REST APIs
- ASP.NET applications
- Internal enterprise portals

It integrates closely with Windows authentication, Active Directory, and Microsoft's web technologies.

---

## Why IIS Matters

Unlike Linux-based web servers, IIS introduces Windows-specific functionality such as:

- ASP.NET
- WebDAV
- NTLM Authentication
- Windows Authentication
- Application Pools

Understanding these features helps security professionals perform more targeted assessments.

---

## IIS Reconnaissance

An IIS assessment typically begins by identifying:

- Server version
- Enabled features
- Authentication methods
- Supported HTTP methods
- Exposed services
- Administrative functionality

These observations guide later vulnerability research.

---

## Assessment Workflow

A structured approach generally includes:

1. Fingerprint the server.
2. Identify enabled services.
3. Enumerate authentication mechanisms.
4. Review configuration.
5. Investigate exposed functionality.

---

## Skills Practiced

- IIS reconnaissance
- Windows web server identification
- Passive fingerprinting
- HTTP analysis
- Attack surface analysis

---

## Key Takeaways

- IIS is Microsoft's primary web server platform.
- Windows-specific technologies create unique attack surfaces.
- Reconnaissance should identify enabled features before testing.
- Accurate fingerprinting improves vulnerability assessment.
- A structured methodology produces more reliable results.