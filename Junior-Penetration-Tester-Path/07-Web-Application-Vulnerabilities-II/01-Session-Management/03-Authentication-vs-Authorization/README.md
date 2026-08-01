# Authentication vs Authorization

## Overview

Authentication and authorisation are two fundamental concepts in web application security that work together to protect user accounts and sensitive resources. Although they are closely related, they serve different purposes within the session management lifecycle.

This lesson explains the difference between authentication and authorisation, describes how they interact with session management, and highlights why both must be correctly implemented to maintain secure web applications.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Differentiate between authentication and authorisation
- Understand how both concepts relate to session management
- Explain the purpose of each security process
- Recognise common security risks associated with weak authentication or authorisation
- Understand why both mechanisms are required for secure access control

---

## Main Content

### What is Authentication?

Authentication is the process of verifying a user's identity.

It answers the question:

> **Who are you?**

Authentication is typically performed using one or more factors, such as:

- Username and password
- Multi-Factor Authentication (MFA)
- Passkeys
- Certificates
- Biometric authentication

Once authentication succeeds, the application creates a session for the user.

---

### What is Authorization?

Authorisation determines what an authenticated user is allowed to access or perform.

It answers the question:

> **What are you allowed to do?**

Typical authorisation decisions include:

- Accessing user profiles
- Viewing administrative pages
- Editing resources
- Deleting data
- Performing privileged operations

Authorisation checks should be performed on every protected request.

---

### Authentication vs Authorization

Although both processes are related, they occur at different stages.

| Authentication | Authorization |
|----------------|---------------|
| Verifies user identity | Verifies user permissions |
| Occurs before access is granted | Occurs whenever protected resources are requested |
| Creates an authenticated session | Uses the session to enforce access control |

Successful authentication does **not** automatically grant permission to access every resource.

---

### Why Both Are Important

A secure application requires both authentication and authorisation.

Weak authentication may allow attackers to impersonate users.

Weak authorisation may allow authenticated users to access resources that belong to someone else or perform actions beyond their assigned privileges.

Both controls must work together throughout the session lifecycle.

---

## Skills Practiced

- Authentication Concepts
- Authorization Concepts
- Session Management
- Access Control
- Web Application Security

---

## Key Takeaways

- Authentication verifies a user's identity.
- Authorization determines what an authenticated user is permitted to access.
- Authentication always occurs before authorisation.
- Every protected request should include server-side authorisation checks.
- Strong session management depends on both secure authentication and effective authorisation.