# Introduction

## Overview

Web servers are the foundation of every web application. They receive client requests, deliver content, and manage communication between users and backend services. Understanding how different web servers operate is an essential skill during reconnaissance, as each server exposes unique characteristics, configuration options, and potential security weaknesses.

This room introduces several commonly deployed web servers and demonstrates how to identify them through passive reconnaissance techniques.

---

## Learning Objectives

- Understand the role of web servers
- Learn how to identify common web server software
- Recognise server-specific characteristics
- Explore common configuration weaknesses
- Build a structured web server assessment methodology

---

## What is a Web Server?

A web server is software responsible for processing HTTP and HTTPS requests and delivering resources such as:

- HTML pages
- Images
- CSS files
- JavaScript
- APIs
- Downloads

Different web servers implement these functions differently, creating unique fingerprinting opportunities.

---

## Common Web Servers

Several web servers dominate modern environments, including:

- Python HTTP Server
- Apache HTTP Server
- Nginx
- Node.js (Express)

Each platform has different default configurations, features, and security considerations.

---

## Fingerprinting Web Servers

Before testing for vulnerabilities, analysts should determine which server is in use.

Useful indicators include:

- HTTP response headers
- Default error pages
- Directory structures
- Status pages
- Response behaviour
- Security headers

These observations provide valuable intelligence without requiring intrusive testing.

---

## Why Server Identification Matters

Different web servers expose different attack surfaces.

Knowing the server software helps analysts:

- Research known vulnerabilities
- Identify default configurations
- Detect exposed administrative features
- Prioritise security testing
- Reduce unnecessary scanning

---

## Skills Practiced

- Web server identification
- Passive reconnaissance
- HTTP analysis
- Technology fingerprinting
- Attack surface analysis

---

## Key Takeaways

- Every web application relies on a web server.
- Different servers expose different fingerprinting indicators.
- Passive reconnaissance provides valuable information early in an assessment.
- Correct server identification improves vulnerability research.
- Understanding server behaviour is fundamental to penetration testing.