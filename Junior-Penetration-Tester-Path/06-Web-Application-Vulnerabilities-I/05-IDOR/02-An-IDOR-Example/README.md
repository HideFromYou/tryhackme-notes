# An IDOR Example

## Overview

The simplest form of an Insecure Direct Object Reference (IDOR) occurs when a web application uses a user-supplied identifier to retrieve a resource without verifying whether the authenticated user has permission to access it. If the application trusts the identifier instead of enforcing proper authorisation, users may gain access to resources that belong to others.

This lesson demonstrates how missing server-side authorisation checks create IDOR vulnerabilities and explains why validating user permissions is more important than trusting object identifiers.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how a basic IDOR vulnerability occurs
- Explain why modifying object identifiers can expose protected resources
- Differentiate between authentication and authorisation failures
- Recognise the risks associated with missing access control
- Understand the importance of server-side permission checks

---

## Main Content

### Direct Object References

Many web applications identify resources using object references such as:

- User IDs
- Order numbers
- Document identifiers
- Ticket numbers
- Profile IDs

These identifiers allow the application to locate the requested resource within its database.

---

### Missing Authorisation

An IDOR vulnerability occurs when the application retrieves a requested object without verifying that the authenticated user owns or is permitted to access it.

Instead of validating permissions, the server simply trusts the identifier supplied by the client.

---

### Potential Impact

Depending on the affected functionality, missing authorisation checks may allow unauthorised users to:

- View sensitive information
- Modify another user's data
- Delete protected resources
- Access private documents
- Perform actions on behalf of other users

The severity depends on the functionality exposed by the vulnerable endpoint.

---

### Preventing IDOR

Applications should never rely solely on object identifiers when making authorisation decisions.

Secure implementations should verify:

- The identity of the authenticated user
- Ownership of the requested object
- User permissions
- Access control policies

Proper server-side authorisation ensures that users can only access resources they are permitted to use.

---

## Skills Practiced

- IDOR Analysis
- Broken Access Control
- Authorisation Validation
- HTTP Request Analysis
- Web Application Security

---

## Key Takeaways

- Object identifiers should never be trusted as proof of authorisation.
- Every request must include a server-side permission check before accessing protected resources.
- Authentication confirms identity, while authorisation determines access rights.
- Missing access control can lead to significant data exposure and unauthorised actions.