# MERN Stack

## Overview

The MERN stack is one of the most widely used JavaScript web development stacks. It combines MongoDB, Express.js, React, and Node.js to create full-stack web applications using JavaScript across both the frontend and backend.

Because of its popularity, understanding how to identify MERN applications is an important reconnaissance skill for penetration testers.

---

## Learning Objectives

- Understand the components of the MERN stack
- Identify Express.js applications
- Recognise common fingerprinting indicators
- Understand why framework identification matters
- Prepare for framework-specific vulnerability research

---

## What is the MERN Stack?

MERN is an acronym for four technologies:

- MongoDB
- Express.js
- React
- Node.js

Together they provide a complete environment for building modern web applications.

---

## Express.js

Express.js is a lightweight web framework built on Node.js.

It is responsible for:

- Routing requests
- Handling middleware
- Managing sessions
- Processing HTTP requests
- Serving APIs

Many Node.js applications expose Express-specific behaviour that can be identified during reconnaissance.

---

## Fingerprinting Express

Common indicators include:

- `X-Powered-By: Express`
- `connect.sid` session cookies
- Default Express error pages
- Standard middleware behaviour
- Node.js response patterns

These characteristics help identify Express applications without interacting aggressively with the server.

---

## Session Management

Express applications frequently rely on session cookies to maintain user state.

During reconnaissance analysts should examine:

- Cookie names
- Cookie attributes
- Security flags
- Session handling behaviour

Improper cookie configuration may indicate additional security weaknesses.

---

## Why Framework Identification Matters

Once Express has been identified, analysts can focus on:

- Framework-specific vulnerabilities
- Middleware behaviour
- Authentication mechanisms
- Known CVEs
- Version-specific weaknesses

Targeted testing is significantly more efficient than generic vulnerability scanning.

---

## Skills Practiced

- Framework fingerprinting
- Express identification
- HTTP header analysis
- Session cookie inspection
- Passive reconnaissance

---

## Key Takeaways

- MERN applications rely heavily on Express.js.
- HTTP headers frequently reveal framework information.
- Session cookies provide valuable reconnaissance data.
- Correct framework identification supports targeted security testing.
- Passive fingerprinting should always precede exploitation.