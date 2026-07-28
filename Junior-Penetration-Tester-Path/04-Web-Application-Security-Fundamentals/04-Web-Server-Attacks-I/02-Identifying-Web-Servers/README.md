# Identifying Web Servers

## Overview

Before investigating vulnerabilities, security professionals first determine which web server is hosting the application. Most servers reveal identifiable characteristics through HTTP responses, making server identification one of the earliest reconnaissance activities during a web assessment.

---

## Learning Objectives

- Understand web server fingerprinting
- Identify common HTTP response indicators
- Recognise server-specific behaviour
- Learn passive identification techniques

---

## HTTP Response Headers

HTTP response headers frequently disclose information about the server software.

Common headers include:

- Server
- X-Powered-By
- Date
- Content-Type
- Cache-Control

Some servers expose software names and version numbers, while others intentionally suppress this information.

---

## Server Banners

A server banner identifies the web server software responsible for processing requests.

Examples include:

- Apache
- Nginx
- Microsoft IIS
- Python HTTP Server

Version information, when available, assists with vulnerability research.

---

## Additional Fingerprinting Techniques

Beyond response headers, analysts may examine:

- Default error pages
- Redirect behaviour
- Cookie names
- Supported HTTP methods
- Directory listings
- Status endpoints

Combining several observations increases confidence in the identified technology.

---

## Security Considerations

Information disclosure is not always a vulnerability, but unnecessary exposure increases reconnaissance opportunities for attackers.

Administrators often reduce exposed information by:

- Hiding version numbers
- Removing unnecessary headers
- Disabling default pages
- Restricting status interfaces

---

## Skills Practiced

- HTTP header analysis
- Server fingerprinting
- Passive reconnaissance
- Technology identification

---

## Key Takeaways

- Response headers are the fastest method for identifying web servers.
- Multiple indicators provide stronger fingerprinting confidence.
- Version disclosure supports vulnerability research.
- Passive techniques minimise interaction with the target.
- Server identification guides later security testing.