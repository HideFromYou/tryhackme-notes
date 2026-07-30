# Finding CSRF Vulnerabilities

## Overview

Identifying Cross-Site Request Forgery (CSRF) vulnerabilities requires understanding how an application processes state-changing requests and whether it verifies that those requests originate from legitimate user actions. Applications that rely solely on authenticated sessions without additional validation may be susceptible to forged requests.

This lesson introduces a structured approach to recognising potential CSRF vulnerabilities during web application security assessments.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how to identify potential CSRF vulnerabilities
- Recognise application features commonly affected by CSRF
- Explain the importance of request validation
- Identify indicators of missing or weak CSRF protection
- Develop a methodology for assessing CSRF risks

---

## Main Content

### Identifying Sensitive Actions

CSRF primarily targets functionality that changes the state of an application.

Examples include:

- Updating account settings
- Changing passwords
- Performing financial transactions
- Creating or deleting resources
- Managing user permissions

These operations should always receive additional security validation.

---

### Analysing HTTP Requests

During an assessment, testers review how sensitive requests are processed.

Important observations include:

- HTTP request methods
- Request parameters
- Session handling
- Authentication mechanisms
- Presence of request validation controls

Understanding the request structure helps determine whether appropriate protections are in place.

---

### Evaluating CSRF Protections

Modern applications commonly implement mechanisms designed to verify that requests originate from legitimate users.

Security assessments should verify whether these protections are:

- Present
- Properly validated
- Consistently applied
- Resistant to predictable behaviour

Weak or inconsistent implementations may reduce their effectiveness.

---

### Building a Testing Methodology

A structured assessment typically involves:

- Identifying state-changing functionality
- Reviewing request behaviour
- Evaluating session handling
- Verifying request validation
- Recording security observations

Following a consistent methodology improves both accuracy and repeatability during security testing.

---

## Skills Practiced

- CSRF Assessment
- HTTP Request Analysis
- Session Security
- Web Application Security
- Security Testing Methodology

---

## Key Takeaways

- CSRF assessments focus on how applications validate sensitive requests.
- State-changing functionality should always receive additional protection beyond authentication.
- Proper request validation significantly reduces the risk of forged requests.
- A structured testing methodology improves the consistency of web application security assessments.