# Burp Suite Notes

## Overview

Burp Suite is a web application security testing tool used for intercepting, inspecting, modifying, and replaying HTTP requests and responses.

---

## Core Modules Covered

- Proxy
- Repeater
- Inspector

---

## Proxy

Purpose:

Capture browser HTTP/S traffic between the client and target web application.

Practical uses:

- Inspect requests
- Capture authentication flows
- Observe cookies, headers, parameters, and responses
- Forward requests for testing

Key learning:

Proxy acts as a man-in-the-middle between browser and target application.

---

## Repeater

Purpose:

Manually modify and resend HTTP requests to observe application behavior.

Practical uses:

- IDOR testing
- SQL Injection testing
- Header manipulation
- Cookie testing
- Authentication / authorization testing
- Input validation testing

Key learning:

Repeater allows repeated manual testing of server-side behavior by modifying request components.

---

## Inspector

Purpose:

Structured editing interface for HTTP requests and responses.

Editable request areas:

- Method
- Path
- Headers
- Cookies
- Body / parameters

Key learning:

Inspector simplifies request modification without manually editing raw HTTP syntax.

---

## Practical Lab Examples

### Header manipulation

Added custom request header:

FlagAuthorised: True

Purpose:

Test application behavior based on custom authorization-related headers.

---

### Input validation / boundary testing

Modified endpoint path:

/product/3

Testing examples:

/product/-1

Purpose:

Observe backend validation failures and trigger server errors.

---

### UNION SQL Injection

Captured vulnerable request:

GET /about/1

Modified injectable path parameter using UNION-based SQL injection.

Example concept:

/about/0 UNION ALL SELECT notes,NULL,NULL,NULL,NULL FROM people WHERE id=1

Purpose:

Extract sensitive database information by exploiting path-based SQL injection.

---

## Key Learning

Burp workflow:

Capture request → Send to Repeater → Modify vulnerable input → Observe response

Main lesson:

Always identify where user-controlled input exists:

- URL path
- Query parameters
- POST body
- Cookies
- Headers

Payload placement depends on the injection point.
