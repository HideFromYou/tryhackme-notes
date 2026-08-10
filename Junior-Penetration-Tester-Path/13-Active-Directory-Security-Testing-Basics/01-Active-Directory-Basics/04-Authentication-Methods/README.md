# 04 - Authentication in AD

## Overview

Authentication is the process of verifying the identity of a user or computer.

In an Active Directory environment, authentication is essential because users and computers constantly need to prove their identity when accessing domain resources.

Active Directory primarily relies on two authentication protocols:

- Kerberos
- NetNTLM

The following sections explain how these authentication mechanisms work and how they differ.

---

## Authentication in Active Directory

When a user wants to access a resource in a domain environment, the user's identity needs to be verified.

A simplified authentication process is:

```text
User
  |
  | Credentials
  v
Domain Controller
  |
  | Authentication
  v
Identity Verified
  |
  v
Access to Resource
```

Authentication is different from authorization.

### Authentication

Answers:

```text
"Who are you?"
```

### Authorization

Answers:

```text
"What are you allowed to access?"
```

Both are important when analysing Active Directory security.

---

## Active Directory Authentication Protocols

The two main authentication mechanisms covered in this module are:

### Kerberos

Kerberos is the primary authentication protocol used by modern Active Directory environments.

It is based on tickets rather than repeatedly sending a user's password.

### NetNTLM

NetNTLM is a challenge-response authentication protocol used in Windows environments.

It is considered a legacy authentication mechanism compared with Kerberos.

---

## Authentication Flow

A simplified Active Directory authentication process can be represented as:

```text
User
 |
 | Authentication Request
 v
Domain Controller
 |
 | Verify Identity
 v
Authentication Protocol
 |
 +---- Kerberos
 |
 +---- NetNTLM
 |
 v
Authenticated Identity
 |
 v
Resource Access
```

---

## Why Authentication Matters for Security Testing

Authentication is one of the most important areas to understand when performing Active Directory security testing.

If an attacker can obtain, abuse or relay authentication material, this may allow them to access resources as another identity.

Therefore, a penetration tester should understand:

- How authentication works
- Which authentication protocol is being used
- Where authentication material is exposed
- How authentication can be abused
- How authentication attacks can be detected
- How authentication can be secured

---

## Kerberos

Kerberos is the default authentication protocol used by modern Windows Active Directory environments.

Instead of sending a password to every service, Kerberos uses tickets to prove that a user has authenticated.

The main Kerberos components introduced later in the module include:

```text
KDC
TGT
TGS
SPN
```

---

## NetNTLM

NetNTLM uses a challenge-response mechanism.

The client does not simply send the user's password to the server.

Instead, the server provides a challenge and the client generates a response based on the user's authentication material.

A simplified flow is:

```text
Client
  |
  | Authentication Request
  v
Server
  |
  | Challenge
  v
Client
  |
  | Challenge Response
  v
Server
  |
  v
Authentication Result
```

---

## Kerberos vs NetNTLM

| Feature | Kerberos | NetNTLM |
|---|---|---|
| Modern AD authentication | Primary | Legacy |
| Authentication model | Ticket-based | Challenge-response |
| TGT | Yes | No |
| TGS | Yes | No |
| SPN | Yes | No |
| Password directly transmitted | No | No |

---

## Security Perspective

Understanding the authentication mechanism in use is important during enumeration and exploitation.

For example, Kerberos and NetNTLM expose different attack surfaces.

An attacker may look for:

```text
Kerberos
   |
   +-- Tickets
   +-- SPNs
   +-- Authentication weaknesses

NetNTLM
   |
   +-- Challenge/Response
   +-- Credential Relay
   +-- Credential Capture
```

The specific weaknesses and attack techniques are covered in the following lessons.

---

## Key Takeaways

- Authentication verifies the identity of a user or computer.
- Authorization determines what an authenticated identity can access.
- Active Directory uses multiple authentication mechanisms.
- Kerberos is the primary authentication protocol in modern AD environments.
- NetNTLM is a legacy challenge-response authentication mechanism.
- Kerberos uses tickets such as TGTs and TGSs.
- Understanding authentication is essential for Active Directory penetration testing.
- Different authentication protocols introduce different security risks and attack opportunities.