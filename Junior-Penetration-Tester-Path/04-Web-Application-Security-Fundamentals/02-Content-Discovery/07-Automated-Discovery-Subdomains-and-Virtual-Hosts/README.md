# Automated Discovery - Subdomains & Virtual Hosts

## Overview

Large organisations often operate multiple websites and services under the same domain. Enumerating subdomains and virtual hosts helps identify additional applications that may not be visible from the primary website.

---

## Learning Objectives

- Understand subdomain enumeration
- Learn the difference between subdomains and virtual hosts
- Explore DNS-based discovery
- Identify additional web applications

---

## Subdomains

A subdomain is a separate hostname associated with a parent domain through DNS.

Examples include:

- blog.example.com
- api.example.com
- dev.example.com
- shop.example.com

Each subdomain may host an independent application with its own functionality and security posture.

---

## DNS Enumeration

DNS enumeration attempts to discover valid subdomains by querying candidate names from a wordlist.

Finding additional subdomains helps expand the attack surface and identify services that may otherwise remain hidden.

---

## Virtual Hosts

Virtual hosts allow multiple websites to share a single IP address.

The web server determines which website to serve based on the HTTP `Host` header rather than the destination IP address.

As a result, virtual hosts may exist even when no public DNS record is available.

---

## Why Enumeration Matters

Different subdomains may contain:

- Development environments
- Administrative portals
- Internal applications
- APIs
- Legacy services

Each discovered host should be considered a separate target during reconnaissance.

---

## Enumeration Workflow

A complete workflow generally includes:

1. Discover subdomains
2. Verify active hosts
3. Identify virtual hosts
4. Inspect discovered applications
5. Continue with targeted reconnaissance

---

## Skills Practiced

- DNS enumeration
- Virtual host discovery
- Attack surface expansion
- Automated reconnaissance

---

## Key Takeaways

- Subdomains often expose additional applications.
- Virtual hosts may exist without public DNS records.
- DNS and virtual host enumeration complement each other.
- Every discovered host should be investigated individually.
- Enumeration improves overall visibility of the target environment.