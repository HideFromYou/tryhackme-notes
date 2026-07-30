# DOM-Based XSS (Client-Side)

## Overview

DOM-Based Cross-Site Scripting (DOM-Based XSS) is a client-side vulnerability that occurs when JavaScript running in the browser processes untrusted data and inserts it into the Document Object Model (DOM) without appropriate validation or encoding. Unlike Reflected and Stored XSS, the vulnerable behaviour exists entirely within the browser and may not involve the server generating malicious content.

This lesson introduces DOM-Based XSS, explains how insecure client-side code can create vulnerabilities, and highlights the importance of secure DOM manipulation.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what DOM-Based XSS is
- Explain how client-side JavaScript can introduce security vulnerabilities
- Recognise common sources of untrusted data in the browser
- Understand why secure DOM manipulation is important
- Identify defensive techniques used to reduce DOM-Based XSS risk

---

## Main Content

### What is DOM-Based XSS?

DOM-Based XSS occurs when client-side JavaScript reads untrusted data and writes it into the page in an unsafe manner.

In this scenario, the browser itself introduces the vulnerability through its handling of the Document Object Model rather than through the server's response.

---

### The Role of the DOM

The Document Object Model (DOM) represents the structure of a web page and allows JavaScript to dynamically modify content.

Applications frequently use the DOM to:

- Update page elements
- Display user information
- Process URL data
- Build interactive interfaces
- Modify page content without reloading

Improper handling of user-controlled data during these operations can create client-side security risks.

---

### Sources of Untrusted Data

Client-side applications may receive user-controlled information from multiple locations, including:

- URL parameters
- URL fragments
- Form input
- Browser storage
- Messages exchanged between browser components

Any untrusted data should be validated before being inserted into the DOM.

---

### Preventing DOM-Based XSS

Secure client-side development focuses on preventing untrusted input from becoming executable content.

Recommended practices include:

- Validating user input
- Using safe DOM manipulation methods
- Applying context-aware output encoding
- Avoiding unsafe insertion of dynamic content
- Implementing Content Security Policy (CSP)

Following secure coding principles significantly reduces the likelihood of DOM-Based XSS vulnerabilities.

---

## Skills Practiced

- DOM-Based XSS Fundamentals
- Client-Side Security
- DOM Manipulation Concepts
- JavaScript Security
- Web Application Security

---

## Key Takeaways

- DOM-Based XSS originates from insecure client-side JavaScript rather than the server.
- Untrusted browser data should never be inserted into the DOM without appropriate protection.
- Secure DOM manipulation is essential for preventing client-side code injection.
- Proper validation, safe APIs, and layered security controls help reduce the risk of DOM-Based XSS.