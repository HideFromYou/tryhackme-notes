# Nginx

## Overview

Nginx is a high-performance web server commonly used as a reverse proxy, load balancer, and web application server. It is widely deployed because of its efficiency, scalability, and ability to handle large volumes of concurrent connections.

Understanding Nginx behaviour helps analysts recognise common configuration issues and identify exposed administrative features.

---

## Learning Objectives

- Understand the purpose of Nginx
- Identify Nginx deployments
- Learn common fingerprinting indicators
- Recognise default configuration issues
- Understand common security considerations

---

## What is Nginx?

Nginx provides several core capabilities, including:

- Static content delivery
- Reverse proxy services
- Load balancing
- SSL/TLS termination
- HTTP caching

Its architecture is designed to support high-performance web environments.

---

## Fingerprinting Nginx

Common indicators include:

- `Server: nginx`
- Default error pages
- Response behaviour
- Configuration-specific headers
- HTTP response patterns

Version information may also be available depending on server configuration.

---

## Autoindex

Nginx can generate directory listings when autoindex is enabled.

Exposed directories may contain:

- Documents
- Application files
- Downloads
- Backup files
- Source code

Directory indexing should only be enabled when intentionally required.

---

## Status Pages

Nginx supports status modules that expose operational information.

These pages may include:

- Active connections
- Request statistics
- Worker processes
- Server performance

Access should be restricted to trusted administrators.

---

## Security Considerations

When assessing Nginx deployments, analysts should review:

- Server headers
- Directory indexing
- Status pages
- Security headers
- Reverse proxy configuration

Proper configuration significantly reduces unnecessary exposure.

---

## Skills Practiced

- Nginx fingerprinting
- HTTP analysis
- Directory exposure assessment
- Passive reconnaissance

---

## Key Takeaways

- Nginx is commonly used in high-performance web environments.
- Autoindex may unintentionally expose sensitive files.
- Status pages should never be publicly accessible.
- Passive fingerprinting quickly identifies Nginx deployments.
- Proper configuration is essential for secure production environments.