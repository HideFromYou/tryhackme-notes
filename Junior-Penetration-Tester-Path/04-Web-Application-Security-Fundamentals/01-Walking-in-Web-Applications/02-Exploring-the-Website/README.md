# Exploring the Website

## Overview

Exploring a website is one of the most important stages of web application reconnaissance. Before attempting to identify vulnerabilities, a penetration tester should understand how the application is structured, what functionality is available, and how users interact with different components.

---

## Learning Objectives

- Learn how to manually enumerate a web application
- Identify accessible functionality
- Discover application entry points
- Understand how information is exposed through navigation
- Build an initial attack surface map

---

## Website Enumeration

Begin by navigating through every available page instead of immediately launching automated tools.

Common areas to inspect include:

- Home page
- About page
- Login page
- Registration page
- Contact page
- Blog or news section
- Search functionality
- User profile pages
- Administration portals

Each page may expose useful information about the application's functionality.

---

## Navigation Analysis

Pay attention to how users move throughout the application.

Look for:

- Navigation menus
- Footer links
- Sidebar menus
- Breadcrumb navigation
- Internal hyperlinks
- Redirects

Hidden or forgotten links can often reveal additional functionality.

---

## URL Inspection

URLs often reveal how the application is organized.

Examples include:

- Static pages
- Dynamic routes
- Query parameters
- Resource identifiers

Example:

```
https://example.com/profile?id=15
```

Interesting parameters may later become targets for security testing.

---

## Forms and User Input

Every form represents a potential interaction point.

Common examples include:

- Login forms
- Registration forms
- Search fields
- Contact forms
- Password reset pages
- Comment sections

Understanding user input locations helps prepare for future testing.

---

## Publicly Available Information

While exploring the website, collect information such as:

- Email addresses
- Usernames
- Company names
- Technologies used
- Internal page names
- File names
- Public documents

Small pieces of information can become valuable during later reconnaissance.

---

## Documentation

Record everything discovered during exploration, including:

- Interesting URLs
- Available functionality
- Parameters
- User roles
- Authentication requirements
- Observed behaviours

Good documentation improves the efficiency of future penetration testing.

---

## Skills Practiced

- Manual website enumeration
- Navigation analysis
- Endpoint discovery
- Information gathering
- Attack surface mapping

---

## Key Takeaways

- Explore every accessible page before testing.
- Understand how users interact with the application.
- Document URLs, parameters, and available functionality.
- Publicly exposed information can support later attack phases.
- Thorough reconnaissance leads to more effective security assessments.