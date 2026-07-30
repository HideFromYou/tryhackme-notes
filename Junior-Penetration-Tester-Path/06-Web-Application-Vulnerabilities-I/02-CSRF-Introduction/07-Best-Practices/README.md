# Best Practices

## Overview

Preventing Cross-Site Request Forgery (CSRF) requires more than a single security control. Modern web applications should implement multiple defensive mechanisms that verify the legitimacy of sensitive requests while protecting authenticated user sessions.

This lesson introduces the best practices commonly used to reduce the risk of CSRF vulnerabilities and strengthen the overall security of web applications.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the importance of layered CSRF protection
- Explain the role of CSRF tokens
- Recognise secure session management practices
- Understand browser-based security mechanisms
- Identify best practices for protecting sensitive application functionality

---

## Main Content

### Implement Strong CSRF Tokens

Applications should generate unique, unpredictable CSRF tokens for sensitive requests and validate them on the server before processing user actions.

Proper token management helps ensure that requests originate from legitimate user interactions.

---

### Validate Request Origin

Applications should verify where sensitive requests originate by using mechanisms such as Origin or Referer header validation when appropriate.

Additional verification helps distinguish legitimate requests from potentially forged ones.

---

### Use Secure Cookie Settings

Modern browsers support security features that help reduce CSRF risk.

Appropriate cookie attributes, including SameSite settings, limit when authentication cookies are automatically included in cross-site requests.

---

### Protect Sensitive Operations

High-risk functionality should receive additional protection beyond standard authentication.

Examples include:

- Password changes
- Account management
- Financial transactions
- Administrative actions
- Permission changes

Critical operations may also require user confirmation or re-authentication.

---

### Apply Defence in Depth

No single security mechanism completely eliminates CSRF risk.

Applications should combine multiple protective measures, including:

- CSRF tokens
- Secure session management
- Request origin validation
- SameSite cookies
- User verification for critical actions
- Regular security testing

Layering security controls significantly improves overall resilience against CSRF attacks.

---

## Skills Practiced

- CSRF Mitigation
- Session Security
- Secure Request Validation
- Web Application Security
- Defence in Depth

---

## Key Takeaways

- Effective CSRF protection requires multiple security controls working together.
- Strong, unpredictable CSRF tokens remain one of the primary defensive mechanisms.
- Browser security features can further reduce the risk of forged requests.
- Sensitive application functionality should always receive additional protection beyond authentication alone.
- Following security best practices significantly improves the resilience of modern web applications.