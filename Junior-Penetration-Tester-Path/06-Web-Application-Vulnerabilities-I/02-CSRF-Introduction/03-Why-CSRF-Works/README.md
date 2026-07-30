# Why CSRF Works

## Overview

Cross-Site Request Forgery succeeds because web applications often trust requests that include valid authentication credentials without verifying whether the request was intentionally initiated by the user. Modern browsers automatically attach session information to requests, making authenticated sessions a potential target if additional protections are not implemented.

This lesson explains the conditions required for a successful CSRF attack and why secure request validation is essential for protecting sensitive application functionality.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand why CSRF attacks are possible
- Explain the relationship between browsers, sessions, and authentication
- Identify the conditions required for a successful CSRF attack
- Recognise common weaknesses in request validation
- Understand why additional security mechanisms are necessary

---

## Main Content

### Automatic Session Handling

After a user authenticates to a web application, the browser automatically includes the associated session information with future requests.

This behaviour improves usability by allowing users to remain logged in without repeatedly entering their credentials.

---

### Trusting Browser Requests

Many applications assume that any request containing valid authentication credentials originates from the legitimate user.

Without additional verification, the server cannot reliably determine whether the request was intentionally submitted or triggered by an external source.

---

### Conditions for CSRF

Several conditions typically exist before a CSRF attack becomes possible:

- The victim is authenticated to the target application
- The browser automatically sends valid session credentials
- Sensitive actions can be performed through predictable requests
- The application lacks sufficient request validation

When these conditions are present, attackers may attempt to trigger unintended actions through the victim's browser.

---

### The Importance of Request Validation

Authentication confirms who the user is, but it does not confirm whether each request was intentionally initiated by that user.

Effective CSRF protection requires applications to verify the legitimacy of sensitive requests before processing them.

---

## Skills Practiced

- Session Security
- Authentication Concepts
- Request Validation
- Web Application Security
- CSRF Risk Assessment

---

## Key Takeaways

- CSRF succeeds because browsers automatically include authentication credentials with requests.
- Authentication alone does not prove that a request was intentionally initiated by the user.
- Applications should verify the authenticity of sensitive requests before processing them.
- Understanding why CSRF works is essential for implementing effective defensive mechanisms.