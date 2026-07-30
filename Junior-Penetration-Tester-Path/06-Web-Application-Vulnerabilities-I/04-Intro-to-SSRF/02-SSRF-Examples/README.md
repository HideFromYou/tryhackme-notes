# SSRF Examples

## Overview

Server-Side Request Forgery (SSRF) vulnerabilities can appear in many forms depending on how a web application constructs server-side requests. While some applications accept a complete URL from the user, others build requests using hostnames, paths, or hidden parameters. Understanding these patterns helps security professionals recognise potential SSRF attack surfaces during web application assessments.

This lesson introduces several common SSRF scenarios and explains how different application designs may unintentionally expose server-side request functionality.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Recognise common SSRF attack vectors
- Understand how applications build server-side requests
- Identify features that may introduce SSRF vulnerabilities
- Explain why user-controlled request destinations are dangerous
- Develop a methodology for analysing potential SSRF functionality

---

## Main Content

### Full URL Parameters

Some applications allow users to provide an entire URL that the server later requests.

Examples include:

- URL preview services
- PDF generators
- Webhook integrations
- Content import features

If the supplied destination is not properly validated, attackers may influence where the server sends requests.

---

### Partial URL Construction

In some applications, users control only part of the destination, such as:

- Hostnames
- Subdomains
- API endpoints
- URL paths

Although developers may believe this reduces risk, insufficient validation can still allow unintended server-side requests.

---

### Path Manipulation

Applications sometimes combine user input with predefined URL structures.

Improper handling of path components may allow requests to reach unintended locations within the application or internal infrastructure.

Careful validation of user-controlled paths helps reduce this risk.

---

### Hidden Request Parameters

Not all SSRF vectors are visible in the browser's address bar.

Applications may store request destinations within:

- Hidden form fields
- API requests
- Background service calls
- Client-side configuration values

Security assessments should examine all user-controllable parameters that influence server-side communication.

---

### Identifying SSRF Patterns

When analysing an application, security professionals should look for features that require the server to retrieve external resources.

Examples include:

- Image fetching
- Document generation
- URL previews
- Webhook delivery
- File import functionality

Any feature that performs outbound requests may represent a potential SSRF attack surface if user input influences the destination.

---

## Skills Practiced

- SSRF Identification
- HTTP Request Analysis
- URL Validation Concepts
- Web Application Security
- Attack Surface Analysis

---

## Key Takeaways

- SSRF vulnerabilities can appear in many different application features.
- User-controlled request destinations should always be carefully validated.
- Hidden parameters and background requests may also introduce SSRF risks.
- Understanding how applications construct server-side requests is essential for identifying potential vulnerabilities.