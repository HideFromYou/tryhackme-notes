# Introduction

## Overview

Server-Side Request Forgery (SSRF) is a web application vulnerability that allows an attacker to influence a server into making unintended HTTP requests. Instead of communicating directly with a target, the attacker abuses the application's functionality to send requests on the server's behalf, potentially accessing resources that are normally unavailable from outside the internal network.

This lesson introduces the fundamentals of SSRF, explains its different forms, and highlights the potential impact on internal infrastructure and cloud environments.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Define Server-Side Request Forgery (SSRF)
- Differentiate between Regular and Blind SSRF
- Understand why SSRF vulnerabilities are dangerous
- Recognise the potential impact on internal systems
- Explain why trusted server-side requests create security risks

---

## Main Content

### What is SSRF?

Server-Side Request Forgery (SSRF) occurs when a web application allows user-controlled input to determine where the server sends an HTTP request.

Because the request originates from the application server, it is often treated as trustworthy by internal services that are inaccessible from the public internet.

---

### Types of SSRF

SSRF vulnerabilities generally fall into two categories:

- **Regular SSRF** – The application's response includes the data returned from the server-side request, allowing the user to view the result directly.
- **Blind SSRF** – The application performs the request but does not return the response, requiring indirect methods to determine whether the request was successful.

Both forms represent significant security risks despite their different behaviours.

---

### Why SSRF Matters

Internal systems often trust requests coming from application servers.

As a result, SSRF vulnerabilities may allow access to:

- Internal administrative interfaces
- Backend APIs
- Monitoring services
- Cloud metadata services
- Other network resources that are not publicly accessible

The overall impact depends on what the application server is permitted to access.

---

### Security Considerations

The severity of SSRF extends beyond a single vulnerable application.

Successful exploitation may expose:

- Sensitive information
- Internal network architecture
- Cloud infrastructure details
- Authentication tokens
- Configuration data

Understanding how applications generate server-side requests is essential for identifying and mitigating SSRF vulnerabilities.

---

## Skills Practiced

- SSRF Fundamentals
- HTTP Request Analysis
- Internal Network Security
- Cloud Security Concepts
- Web Application Security

---

## Key Takeaways

- SSRF allows attackers to influence server-side HTTP requests.
- Requests originating from trusted servers may access protected internal resources.
- Regular and Blind SSRF differ in how responses are exposed to the attacker.
- Internal infrastructure and cloud services are common SSRF targets.
- Secure request validation and careful application design are essential for preventing SSRF vulnerabilities.