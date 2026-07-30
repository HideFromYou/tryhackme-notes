# Where are IDORs Located?

## Overview

Insecure Direct Object Reference (IDOR) vulnerabilities can appear anywhere a web application references an object using user-supplied data. They are not limited to URLs and may exist in API requests, form submissions, cookies, or other application components that interact with protected resources.

This lesson explores common locations where IDOR vulnerabilities may occur and explains why every request involving protected data requires proper server-side authorisation.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify common locations where IDOR vulnerabilities can occur
- Understand how object references are used throughout web applications
- Recognise why every resource request requires authorisation
- Explain why client-controlled data should never determine access rights
- Understand secure access control practices

---

## Main Content

### Common Locations for IDOR

Applications frequently reference protected resources using identifiers supplied by the client.

Common locations include:

- URL parameters
- REST API endpoints
- Form fields
- JSON request bodies
- Cookies
- Hidden HTML fields

Any location containing an object reference should be treated as a potential access control boundary.

---

### APIs and Modern Applications

Modern web applications often rely heavily on APIs to retrieve and modify data.

Each API endpoint that accesses protected resources should verify:

- The identity of the authenticated user
- Resource ownership
- Assigned permissions
- Access control policies

Authorisation should be enforced consistently across all API endpoints.

---

### Client-Controlled Data

Applications should never trust values received from the client when making access control decisions.

Even if identifiers are:

- Hidden
- Encoded
- Hashed
- Randomly generated

the server must independently verify that the user is authorised to access the requested resource.

---

### Secure Access Control

Strong access control should be applied consistently throughout the application.

Recommended practices include:

- Server-side authorisation checks
- Ownership validation
- Role-based access control
- Least privilege principles
- Consistent permission enforcement across every endpoint

Every request involving protected resources should be validated before data is returned or modified.

---

## Skills Practiced

- IDOR Identification
- Access Control Analysis
- API Security Fundamentals
- Web Application Security
- Secure Authorisation

---

## Key Takeaways

- IDOR vulnerabilities can appear anywhere user-controlled object references are processed.
- URLs are only one possible location where IDOR issues may exist.
- APIs, forms, cookies, and request bodies also require proper authorisation.
- Secure applications validate every request using server-side access control rather than trusting client-supplied identifiers.