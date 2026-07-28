# Python HTTP Server

## Overview

Python includes a lightweight built-in HTTP server that is commonly used during development, testing, and file sharing. While convenient, it lacks many security features found in production-grade web servers and should not be exposed to untrusted environments.

---

## Learning Objectives

- Understand the purpose of Python's built-in HTTP server
- Identify Python HTTP Server deployments
- Recognise common security limitations
- Learn why development servers should not be used in production

---

## What is Python HTTP Server?

Python's built-in HTTP server provides a simple way to serve files directly from a local directory.

Typical use cases include:

- Development
- Testing
- File sharing
- Demonstrations
- Temporary hosting

It is designed for simplicity rather than security.

---

## Default Behaviour

By default, the server exposes the contents of the directory from which it is started.

Depending on configuration, users may be able to:

- Browse directories
- Download files
- Access subdirectories
- View static content

Proper file placement is therefore important.

---

## Fingerprinting

Common indicators include:

- Python-specific server banners
- Default directory listings
- Simple response behaviour
- Minimal configuration options

These characteristics help distinguish the server from production platforms.

---

## Security Considerations

Development servers generally lack advanced security features such as:

- Authentication
- Access control
- Rate limiting
- Security headers
- Request filtering

They should only be used in trusted environments.

---

## Skills Practiced

- Python server identification
- Passive fingerprinting
- Directory exposure analysis
- Security assessment

---

## Key Takeaways

- Python HTTP Server is intended for development and testing.
- Default configurations prioritise simplicity over security.
- Directory exposure should always be reviewed.
- Development servers should never replace production web servers.
- Passive reconnaissance quickly identifies Python-based servers.