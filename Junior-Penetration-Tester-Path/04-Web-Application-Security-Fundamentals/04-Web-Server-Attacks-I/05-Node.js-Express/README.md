# Node.js (Express)

## Overview

Express is the most popular web framework for Node.js and is widely used for modern web applications and REST APIs. Its lightweight architecture and middleware system make it flexible and efficient, but development environments can unintentionally expose valuable information during reconnaissance.

---

## Learning Objectives

- Understand the Express framework
- Identify Express applications
- Learn common fingerprinting indicators
- Recognise development-related information disclosure
- Understand Express security considerations

---

## What is Express?

Express is a minimal web framework built on Node.js.

It provides functionality such as:

- Routing
- Middleware
- Session handling
- API development
- Request processing
- Static content delivery

Its modular design allows developers to build scalable web applications.

---

## Fingerprinting Express

Common indicators include:

- `X-Powered-By: Express`
- Express session cookies
- Default error responses
- Middleware behaviour
- Node.js runtime characteristics

Multiple indicators should be used together for reliable identification.

---

## Development Mode

Development environments often expose additional debugging information.

Examples include:

- Detailed stack traces
- Error messages
- Route information
- Environment details
- Application structure

These disclosures provide valuable reconnaissance data and should not be available in production.

---

## Security Considerations

Administrators should ensure that production deployments:

- Disable debug output
- Hide unnecessary headers
- Protect session cookies
- Implement security middleware
- Validate user input

Proper configuration reduces unnecessary information disclosure.

---

## Skills Practiced

- Express fingerprinting
- HTTP header analysis
- Development environment identification
- Passive reconnaissance

---

## Key Takeaways

- Express is a widely used Node.js framework.
- Development environments often reveal excessive information.
- Framework identification supports targeted testing.
- Production deployments should minimise information disclosure.
- Passive fingerprinting improves reconnaissance quality.