# Session Management

## Overview

Session Management is a fundamental component of web application security that enables applications to maintain a user's authenticated state across multiple HTTP requests. Since HTTP is a stateless protocol, session management provides a secure method of identifying users, tracking their actions, and enforcing authorisation throughout their interaction with an application.

This room introduces the session management lifecycle, explains the differences between authentication and authorisation, compares cookie-based and token-based session management, examines common implementation weaknesses, and explores best practices for securing user sessions.

---

## Learning Objectives

After completing this room, you should be able to:

- Understand the purpose of session management
- Explain the complete session management lifecycle
- Differentiate between authentication and authorisation
- Compare cookie-based and token-based session management
- Identify common session management vulnerabilities
- Understand best practices for securing user sessions

---

## Lessons

### 1. Introduction

Introduces session management, explains why sessions are required for web applications, and outlines the topics covered throughout the room.

### 2. What is Session Management?

Explores the session management lifecycle, including session creation, tracking, expiry, and termination, and explains how applications maintain user state.

### 3. Authentication vs Authorization

Examines the differences between authentication and authorisation, highlighting how both contribute to secure session management.

### 4. Cookies vs Tokens

Compares the two primary session management approaches, discussing how cookies and tokens work, along with their advantages and limitations.

### 5. Securing the Session Lifecycle

Explains common weaknesses that can occur during each stage of the session lifecycle and introduces defensive techniques used to protect user sessions.

### 6. Exploiting Insecure Session Management

Applies the concepts learned throughout the room by examining practical examples of insecure session management implementations and their security implications.

### 7. Conclusion

Summarises the key concepts covered throughout the room and reviews the most important principles for implementing secure session management.

---

## Skills Practiced

- Session Management
- Authentication
- Authorisation
- Cookie Security
- Token-Based Authentication
- Session Lifecycle Security
- Web Application Security
- HTTP Security
- Access Control

---

## Tools Used

- Web Browser
- Browser Developer Tools
- Burp Suite
- HTTP Requests
- TryHackMe AttackBox

---

## Key Takeaways

- Session management enables web applications to maintain authenticated user state across stateless HTTP requests.
- Authentication identifies users, while authorisation determines what they are allowed to do.
- Cookies and tokens each provide different approaches to managing user sessions.
- Every phase of the session lifecycle must be secured to prevent session hijacking and related attacks.
- Proper session generation, storage, validation, expiration, and termination are essential components of secure web application design.