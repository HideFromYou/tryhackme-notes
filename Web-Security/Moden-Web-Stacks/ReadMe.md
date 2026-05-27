# Modern Web Stacks Fingerprinting & Exploitation Notes

Practical notes from TryHackMe focused on identifying modern web application stacks, understanding their attack surfaces, and mapping common vulnerabilities.

---

## Overview

Modern web applications are built using different technology stacks.

As a penetration tester, identifying the stack helps prioritize attack paths instead of guessing blindly.

Core methodology:

**Fingerprint → Identify Stack → Understand Attack Surface → Map Common Vulnerabilities → Test**

---

# 1. MERN Stack

## Stack Components

MERN stands for:

- MongoDB
- Express.js
- React
- Node.js

JavaScript-based full-stack architecture.

---

## Fingerprinting Indicators

### HTTP Headers
```http
X-Powered-By: Express
```

---

### Session Cookie
```text
connect.sid
```

---

### Error Response
```text
Cannot GET /nonexistent
```

Express default routing behavior.

---

## Pentester Mindset

Express / Node.js usually means:

- API-heavy applications
- JSON request handling
- Session cookies or JWT authentication
- Custom middleware logic
- MongoDB / NoSQL backend

---

## Common Vulnerabilities

- Prototype Pollution
- NoSQL Injection
- Broken Authentication
- JWT Misconfiguration
- IDOR
- Mass Assignment
- File Upload Issues

---

## Example CVE

### CVE-2020-8203
Prototype pollution leading to authentication bypass.

Impact:

High

---

# 2. Next.js Stack

## Stack Components

Next.js is a React production framework running on Node.js.

Common for:

- Dashboards
- SaaS platforms
- Customer portals
- Modern React apps

---

## Fingerprinting Indicators

### HTTP Headers
```http
X-Powered-By: Next.js
```

---

### Static Asset Paths
```text
/_next/static/chunks/
```

---

### HTML Source
```javascript
window.__next_f
```

App Router indicator.

---

### Framework Headers
```text
x-nextjs-cache
x-nextjs-prerender
x-nextjs-stale-time
```

---

## Pentester Mindset

Next.js often means:

- Middleware-based auth
- React frontend
- API routes
- Server-side rendering
- Framework-specific attack surface

---

## Common Vulnerabilities

- Middleware auth bypass
- Broken access control
- Framework-specific CVEs
- API auth flaws
- Header trust issues

---

## Example CVE

### CVE-2025-29927
Middleware authentication bypass using:

```http
x-middleware-subrequest
```

Impact:

Critical

---

# 3. Django Stack

## Stack Components

Python-based web framework.

Common stack:

- Python
- Django
- PostgreSQL / MySQL
- Gunicorn / WSGI
- NGINX

---

## Fingerprinting Indicators

### Cookie
```text
csrftoken
```

---

### Hidden Form Field
```html
csrfmiddlewaretoken
```

Strong Django fingerprint.

---

### Server Header
```http
Server: WSGIServer/0.2 CPython/X.X.X
```

---

### Security Headers
```http
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Referrer-Policy: same-origin
```

---

## Pentester Mindset

Django suggests:

- Python backend logic
- ORM usage
- CSRF protection
- Admin panels
- Potential debug mode leaks

---

## Common Vulnerabilities

- SQL Injection (unsafe raw SQL)
- Debug Information Disclosure
- Authentication Logic Flaws
- Template Injection
- Admin Exposure

---

## Example CVE

### CVE-2021-35042
SQL injection through unsafe ORDER BY query construction.

Impact:

Critical

---

# 4. LAMP Stack

## Stack Components

LAMP stands for:

- Linux
- Apache
- MySQL
- PHP

Classic web stack.

---

## Fingerprinting Indicators

### Server Header
```http
Server: Apache/2.4.49 (Unix)
```

---

### Error Pages
404 responses leaking Apache version.

---

### CGI Path
```text
/cgi-bin/
```

403 indicates CGI exists and execution may be enabled.

---

## Pentester Mindset

LAMP often suggests:

- Legacy applications
- PHP backend
- File-based web apps
- Classic infrastructure exposure

---

## Common Vulnerabilities

- LFI
- RFI
- SQL Injection
- File Upload RCE
- Directory Traversal
- Misconfigured CGI
- Legacy CVEs

---

## Example CVE

### CVE-2021-41773
Apache path traversal leading to RCE with mod_cgi.

Impact:

Critical

---

# 5. Automation with Nikto

Nikto helps automate initial web fingerprinting.

Example:

```bash
nikto -h http://TARGET
```

Useful for:

- Stack identification
- Header analysis
- Known misconfigurations
- Version disclosure
- Missing security headers

---

## What Nikto Finds

Examples:

- Express fingerprints
- Django headers
- Apache versions
- TRACE enabled
- Missing X-Frame-Options
- Cookie security issues

---

## Limitation

Nikto does NOT replace manual testing.

It misses:

- Business logic flaws
- IDOR
- Prototype Pollution
- Custom auth bugs
- Deep application vulnerabilities

---

# 6. Core Pentesting Methodology

## Step 1 — Fingerprint

Identify:

- Framework
- Backend language
- Web server
- Authentication model
- Stack version

Questions:

- Is this Express?
- Is this Django?
- Is this Apache?
- Is this Next.js?

---

## Step 2 — Understand Attack Surface

Look for:

- APIs
- Forms
- Headers
- Cookies
- Sessions
- Hidden parameters
- File uploads
- Admin routes

---

## Step 3 — Map Likely Vulnerabilities

Examples:

Express:
- Prototype Pollution
- NoSQL Injection

Django:
- Raw SQL misuse
- Debug leaks

Next.js:
- Middleware bypass
- Framework auth flaws

Apache:
- Traversal
- CGI abuse
- Legacy RCE

---

## Step 4 — Research & Test

Real pentesting is not memory-only.

Workflow:

- Recognize stack
- Build hypotheses
- Research known issues
- Validate manually
- Exploit when confirmed

---

# Key Takeaways

- Every stack leaks fingerprints
- Framework identity changes attack strategy
- Technology recognition improves testing efficiency
- Automation helps, manual analysis wins
- Pentesting is methodology + research, not pure memorization
