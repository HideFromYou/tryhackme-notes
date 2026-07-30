# A Practical IDOR Example

## Overview

IDOR vulnerabilities become particularly dangerous when they expose real user data or allow unauthorised actions. In practice, these vulnerabilities are often discovered by analysing how an application references resources and determining whether proper authorisation checks are performed after a request is received.

This lesson demonstrates the typical characteristics of an IDOR vulnerability from a defender's perspective and reinforces the importance of validating permissions for every protected resource.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how IDOR vulnerabilities appear in real-world applications
- Recognise common scenarios where IDORs may exist
- Explain why server-side authorisation is essential
- Identify secure design principles that prevent IDOR
- Understand the impact of broken access control

---

## Main Content

### Real-World IDOR Scenarios

IDOR vulnerabilities commonly affect application features that allow users to access or manage personal resources.

Examples include:

- User profiles
- Orders and purchases
- Support tickets
- Uploaded documents
- Medical records
- Financial information
- Private messages

Each of these resources should only be accessible to authorised users.

---

### The Root Cause

The underlying issue is not the identifier itself, but the absence of proper authorisation.

A vulnerable application may correctly identify the requested resource but fail to verify whether the authenticated user has permission to access or modify it.

This results in a Broken Access Control vulnerability.

---

### Potential Business Impact

Successful exploitation of an IDOR vulnerability can lead to:

- Disclosure of confidential information
- Unauthorised modification of records
- Deletion of sensitive data
- Privacy violations
- Regulatory compliance issues
- Loss of customer trust

The overall impact depends on the sensitivity of the affected resources.

---

### Preventing Practical IDOR Vulnerabilities

Secure applications should implement access control consistently across every feature.

Recommended practices include:

- Validate user permissions on every request
- Verify ownership before returning resources
- Apply role-based or attribute-based access control
- Follow the principle of least privilege
- Perform regular security testing of access control mechanisms

Access control should always be enforced on the server, regardless of how identifiers are generated or presented to users.

---

## Skills Practiced

- IDOR Analysis
- Broken Access Control
- Authorisation Validation
- Secure Application Design
- Web Application Security

---

## Key Takeaways

- Practical IDOR vulnerabilities result from missing or insufficient server-side authorisation checks.
- Sensitive resources should always be protected by robust access control policies.
- Identifier complexity does not replace proper authorisation.
- Consistent server-side permission validation is the most effective defence against IDOR vulnerabilities.