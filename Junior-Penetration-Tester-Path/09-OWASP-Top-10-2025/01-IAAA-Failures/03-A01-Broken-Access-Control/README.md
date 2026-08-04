# A01 - Broken Access Control

## Overview

**Broken Access Control** occurs when an application fails to properly enforce **who can access which resources** on every server-side request. Instead of validating whether a user is authorized to access a resource, the application trusts information supplied by the client, allowing attackers to access or modify data that belongs to other users.

A common example is **Insecure Direct Object Reference (IDOR)**, where simply changing an identifier in a URL (e.g., `?id=7` → `?id=6`) allows access to another user's data. This can result in either **horizontal** or **vertical privilege escalation**, depending on the resources accessed. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Broken Access Control is
- Explain how IDOR vulnerabilities occur
- Differentiate between horizontal and vertical privilege escalation
- Recognize why server-side authorization is essential
- Identify common access control weaknesses

---

## Main Content

### What is Broken Access Control?

Broken Access Control occurs when the server does not verify whether a user is authorized to access a requested resource.

Instead of enforcing permissions on every request, the application relies on information supplied by the client, allowing unauthorized access to protected resources. :contentReference[oaicite:1]{index=1}

---

### Insecure Direct Object Reference (IDOR)

One of the most common examples of Broken Access Control is **IDOR**.

For example:

```text
/account?id=7
```

If changing the identifier to:

```text
/account?id=6
```

displays another user's account information, the application has failed to enforce proper authorization.

This vulnerability exists because the server trusts the user-supplied identifier instead of verifying ownership. :contentReference[oaicite:2]{index=2}

---

### Horizontal Privilege Escalation

**Horizontal privilege escalation** occurs when a user accesses resources belonging to another user who has the **same privilege level**.

Examples include:

- Viewing another customer's profile
- Reading another user's orders
- Editing another user's account

The user's role does not change, but unauthorized data becomes accessible. :contentReference[oaicite:3]{index=3}

---

### Vertical Privilege Escalation

**Vertical privilege escalation** occurs when a user gains access to functionality reserved for users with **higher privileges**.

Examples include:

- Accessing an administrator dashboard
- Modifying administrative settings
- Executing privileged actions

This allows attackers to perform operations beyond their intended permissions. :contentReference[oaicite:4]{index=4}

---

### Preventing Broken Access Control

Applications should:

- Enforce authorization on every server-side request.
- Never trust client-supplied identifiers.
- Verify resource ownership before returning data.
- Apply role-based access control consistently.

Server-side authorization is the primary defense against Broken Access Control vulnerabilities. :contentReference[oaicite:5]{index=5}

---

## Skills Practiced

- Access Control
- IDOR Identification
- Authorization
- Privilege Escalation
- Web Application Security

---

## Key Takeaways

- Broken Access Control occurs when applications fail to enforce authorization checks on every request.
- IDOR vulnerabilities allow attackers to access resources by modifying object identifiers.
- Horizontal privilege escalation affects users with the same role, while vertical privilege escalation targets higher privileges.
- Applications must never trust client-controlled resource identifiers.
- Proper server-side authorization is essential for protecting sensitive application data. :contentReference[oaicite:6]{index=6}