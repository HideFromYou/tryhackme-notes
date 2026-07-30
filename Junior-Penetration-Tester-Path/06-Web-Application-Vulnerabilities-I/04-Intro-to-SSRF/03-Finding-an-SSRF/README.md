# Finding an SSRF

## Overview

Identifying Server-Side Request Forgery (SSRF) vulnerabilities requires understanding which application features cause the server to make outbound requests. Any functionality that retrieves remote resources based on user input should be considered a potential attack surface and carefully evaluated during a security assessment.

This lesson introduces a systematic approach to identifying SSRF vulnerabilities and recognising application behaviour that may allow unintended server-side requests.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify application features that may be vulnerable to SSRF
- Recognise user-controlled input that influences server-side requests
- Understand common SSRF attack surfaces
- Explain how server responses can reveal SSRF behaviour
- Develop a structured methodology for SSRF identification

---

## Main Content

### Identifying Request Functionality

The first step in identifying SSRF is locating functionality where the server retrieves information from another system.

Common examples include:

- URL preview services
- File or image retrieval
- Document generation
- API integrations
- Webhook configurations

Whenever the application communicates with another resource on behalf of the user, SSRF should be considered.

---

### Analysing User Input

Security assessments should determine whether users can influence any part of the destination request.

Areas to examine include:

- Full URLs
- Hostnames
- IP addresses
- URL paths
- Hidden form fields
- API parameters

Even partial control over the request destination may introduce SSRF risk.

---

### Observing Application Behaviour

Application responses often provide clues about server-side request processing.

Useful observations include:

- Differences in response times
- HTTP status codes
- Error messages
- Resource availability
- Changes in application behaviour

These indicators can help identify potential SSRF vulnerabilities, particularly when direct responses are unavailable.

---

### Building an Assessment Methodology

A structured SSRF assessment typically involves:

- Identifying features that perform outbound requests
- Determining whether users influence request destinations
- Analysing request construction
- Observing server responses
- Evaluating existing validation mechanisms

Following a consistent methodology improves both accuracy and repeatability during web application security testing.

---

## Skills Practiced

- SSRF Identification
- HTTP Request Analysis
- Attack Surface Analysis
- Web Application Security
- Security Assessment Methodology

---

## Key Takeaways

- SSRF vulnerabilities originate from application features that make server-side requests.
- User-controlled request destinations should always be treated as potential attack surfaces.
- Response behaviour can reveal valuable information during SSRF assessments.
- A structured testing methodology improves the identification of SSRF vulnerabilities.