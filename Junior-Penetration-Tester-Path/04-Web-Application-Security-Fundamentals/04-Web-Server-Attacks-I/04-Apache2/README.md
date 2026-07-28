# Apache2

## Overview

Apache HTTP Server is one of the most widely deployed web servers in the world. Its flexibility, modular architecture, and extensive configuration options have made it a standard choice for hosting websites and web applications across many environments.

Understanding Apache's default behaviour and common configurations helps penetration testers identify potential security weaknesses during reconnaissance.

---

## Learning Objectives

- Understand Apache HTTP Server
- Identify Apache deployments
- Learn common fingerprinting techniques
- Recognise default features and modules
- Identify common security concerns

---

## What is Apache?

Apache is an open-source web server that supports:

- Static websites
- Dynamic web applications
- Virtual hosts
- Reverse proxy functionality
- SSL/TLS
- Load balancing

Its modular design allows administrators to enable only the functionality required for their environment.

---

## Fingerprinting Apache

Apache commonly reveals itself through:

- `Server` response headers
- Default error pages
- Standard HTTP responses
- Module-specific behaviour
- Directory structures

Version disclosure can significantly simplify vulnerability research.

---

## Common Modules

Apache supports many optional modules.

Frequently encountered examples include:

- mod_status
- mod_rewrite
- mod_ssl
- mod_proxy
- mod_headers

Each module extends the server's capabilities and may introduce additional attack surfaces if improperly configured.

---

## Directory Listing

If directory indexing is enabled, users may browse directory contents when no default page exists.

Directory listings may expose:

- Source code
- Backup files
- Configuration files
- Internal documentation
- Uploaded content

Directory indexing should generally be disabled on production systems.

---

## Server Status

Some Apache deployments expose status pages that provide operational information.

Depending on configuration, these pages may reveal:

- Active connections
- Running workers
- Request statistics
- Server uptime
- Performance metrics

Administrative interfaces should be properly restricted.

---

## Skills Practiced

- Apache fingerprinting
- HTTP analysis
- Module identification
- Directory exposure assessment
- Passive reconnaissance

---

## Key Takeaways

- Apache remains one of the most widely deployed web servers.
- Modules extend functionality but increase complexity.
- Directory listings may expose sensitive information.
- Administrative interfaces should never be publicly accessible.
- Passive reconnaissance provides valuable Apache fingerprinting information.