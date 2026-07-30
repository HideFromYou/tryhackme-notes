# What is CSRF?

## Overview

Cross-Site Request Forgery (CSRF) is a web application vulnerability that tricks an authenticated user's browser into sending unintended requests to a trusted application. Since the browser automatically includes valid session credentials, the application may process these forged requests as though they originated from the legitimate user.

This lesson explains the core principles of CSRF, how these attacks differ from other web vulnerabilities, and why authenticated applications require additional request validation.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Define Cross-Site Request Forgery (CSRF)
- Explain how forged requests are created
- Understand the role of authenticated sessions in CSRF attacks
- Recognise the potential impact of successful CSRF exploitation
- Differentiate CSRF from other common web application vulnerabilities

---

## Main Content

### Understanding CSRF

CSRF occurs when a malicious website, email, or other resource causes a victim's browser to send a request to another website where the user is already authenticated.

Because the request includes valid authentication credentials, the server may accept it as a legitimate user action.

---

### The Role of Authenticated Sessions

Most web applications maintain user sessions after successful authentication.

As long as the session remains active, browsers automatically include the necessary session information with every request. Without additional verification, applications cannot always distinguish between legitimate user actions and forged requests.

---

### Potential Impact

The consequences of a successful CSRF attack depend on the functionality available to the authenticated user.

Possible impacts include:

- Changing account settings
- Modifying stored information
- Performing financial or administrative actions
- Creating or deleting resources
- Triggering unintended application functionality

---

### Why CSRF Is Unique

Unlike attacks that steal authentication credentials, CSRF takes advantage of an already authenticated session.

The attacker does not need to know the victim's password or session identifier; instead, the attack relies on the browser automatically sending valid authentication information.

---

## Skills Practiced

- CSRF Fundamentals
- Session Security
- Web Application Security
- Authentication Concepts
- Request Validation

---

## Key Takeaways

- CSRF exploits the trust between an authenticated browser and a web application.
- Browsers automatically include session credentials with requests, creating opportunities for forged actions.
- Successful CSRF attacks rely on existing authenticated sessions rather than stolen credentials.
- Proper request validation is essential for preventing Cross-Site Request Forgery vulnerabilities.