# Important Terminologies

## Overview

Before understanding how Cross-Site Scripting (XSS) works, it is important to become familiar with the technologies that make modern web applications interactive. XSS relies on how browsers interpret HTML, execute JavaScript, manage user sessions, and manipulate web page content.

This lesson introduces the key concepts and terminology that provide the foundation for understanding client-side security vulnerabilities.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the role of JavaScript in web applications
- Explain what the Document Object Model (DOM) is
- Recognise the purpose of cookies and user sessions
- Understand how URL parameters are processed
- Explain why these technologies are relevant to XSS

---

## Main Content

### JavaScript

JavaScript is the primary programming language executed by web browsers to create interactive and dynamic web applications.

It is responsible for tasks such as:

- Updating page content
- Validating user input
- Handling user interactions
- Communicating with servers
- Modifying the page without requiring a full reload

Because browsers trust JavaScript delivered by web applications, improperly handled user input can sometimes be executed as code.

---

### Document Object Model (DOM)

The Document Object Model (DOM) is the browser's internal representation of a web page.

JavaScript interacts with the DOM to:

- Read page content
- Modify HTML elements
- Update text and images
- Respond to user actions
- Create dynamic interfaces

Many client-side vulnerabilities occur when untrusted data is inserted into the DOM without proper validation.

---

### Cookies

Cookies are small pieces of data stored by the browser that help web applications maintain information between requests.

They are commonly used for:

- User authentication
- Session management
- User preferences
- Tracking activity

Protecting cookies is an important aspect of web application security because they often contain sensitive session information.

---

### Sessions

A session allows a web application to recognise an authenticated user across multiple requests.

After successful authentication, the browser typically sends a session identifier with future requests, allowing the server to associate those requests with the correct user.

Many XSS attacks aim to abuse or compromise authenticated user sessions.

---

### URL Parameters

URL parameters allow information to be passed within a web address.

Applications often use these parameters to:

- Display search results
- Filter content
- Load resources
- Process user input

Improper handling of parameter values can introduce client-side security risks if untrusted data is rendered without appropriate safeguards.

---

## Skills Practiced

- JavaScript Fundamentals
- DOM Concepts
- Session Management
- Browser Security
- Web Application Fundamentals

---

## Key Takeaways

- JavaScript powers the interactive behaviour of modern web applications.
- The DOM provides JavaScript with access to web page content and structure.
- Cookies and sessions enable authenticated user interactions.
- URL parameters frequently carry user-controlled input that must be handled securely.
- Understanding these core concepts is essential before studying Cross-Site Scripting vulnerabilities.