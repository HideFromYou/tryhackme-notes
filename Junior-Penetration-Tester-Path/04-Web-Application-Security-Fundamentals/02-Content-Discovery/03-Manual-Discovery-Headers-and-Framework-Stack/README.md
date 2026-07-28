# Manual Discovery - Headers & Framework Stack

## Overview

HTTP responses contain metadata that reveals how a web application communicates with clients. Examining response headers and identifying the application's technology stack helps analysts understand the environment before beginning security testing.

---

## Learning Objectives

- Understand HTTP response headers
- Identify server technologies
- Learn framework fingerprinting techniques
- Recognise information disclosure through headers

---

## HTTP Headers

Whenever a browser requests a resource, the server returns HTTP headers containing additional information.

Common headers include:

- Server
- Content-Type
- Cache-Control
- Set-Cookie
- Location
- Content-Security-Policy

These values provide insight into application behaviour and configuration.

---

## Server Information

Some servers disclose software details through the `Server` header.

Examples include:

- Apache
- Nginx
- IIS
- LiteSpeed

Version information may also be exposed if not properly configured.

---

## Security Headers

Modern web applications often implement security headers to improve browser security.

Examples include:

- Content-Security-Policy
- Strict-Transport-Security
- X-Frame-Options
- X-Content-Type-Options
- Referrer-Policy

Their presence helps strengthen client-side protections.

---

## Technology Fingerprinting

Framework fingerprinting identifies the technologies used to build the application.

Examples include:

- WordPress
- Drupal
- Joomla
- Laravel
- Django
- React
- Angular
- Vue.js

Knowing the technology stack assists with vulnerability research.

---

## Why Framework Detection Matters

Every framework has its own:

- Default files
- Directory structure
- Configuration patterns
- Security considerations
- Update history

Correctly identifying the framework allows analysts to perform more targeted reconnaissance.

---

## Skills Practiced

- HTTP header analysis
- Technology fingerprinting
- Framework identification
- Manual reconnaissance

---

## Key Takeaways

- HTTP headers reveal valuable metadata.
- Servers may unintentionally disclose software information.
- Security headers provide insight into browser protections.
- Framework identification supports targeted security testing.
- Header analysis is a standard step during reconnaissance.