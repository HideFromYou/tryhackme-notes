# Walking in Web Applications

## Overview

Manual web application reconnaissance is the first step in every web penetration test. Before using automated tools, it is important to understand how an application functions by interacting with it through a web browser. This process helps identify the application's structure, available functionality, and potential attack surface.

---

## Learning Objectives

- Understand the purpose of manual web application reconnaissance
- Learn how users interact with a web application
- Identify common components of modern websites
- Discover exposed functionality before automated testing
- Develop a methodology for exploring web applications

---

## What is a Web Application?

A web application is software that users interact with through a web browser. It consists of two main components:

- **Client-side** – Runs in the user's browser (HTML, CSS, JavaScript).
- **Server-side** – Processes requests, manages data, and returns responses.

Every interaction between the browser and the server creates opportunities for security testing.

---

## Manual Exploration

Before using scanners or vulnerability assessment tools, manually navigate the application to understand its functionality.

Areas worth exploring include:

- Homepage
- Login and registration pages
- Navigation menus
- Search functionality
- Contact forms
- User dashboards
- File upload features
- Administrative sections

Understanding how the application behaves provides valuable context for future testing.

---

## Building the Attack Surface

During reconnaissance, identify every accessible feature that may become a potential attack vector.

Examples include:

- URLs
- Parameters
- Forms
- Buttons
- Search boxes
- File uploads
- Download functionality
- User roles

Documenting these components creates an initial attack surface map.

---

## Why Manual Reconnaissance Matters

Manual exploration often reveals information that automated scanners may overlook, including:

- Hidden pages
- Developer comments
- Client-side validation
- Business logic
- Interesting workflows
- Information disclosure

Strong observation skills are essential for effective penetration testing.

---

## Skills Practiced

- Manual web reconnaissance
- Attack surface mapping
- Browser-based analysis
- Application workflow identification
- Feature enumeration

---

## Key Takeaways

- Always begin with manual exploration before running automated tools.
- Understanding application behaviour improves penetration testing.
- Every page and feature expands the attack surface.
- Careful observation frequently uncovers valuable information.
- Manual reconnaissance provides the foundation for successful web application assessments.