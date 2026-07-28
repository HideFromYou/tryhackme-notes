# Viewing the Page Source

## Overview

Viewing the page source allows penetration testers to inspect the raw HTML delivered by the web server. Although users normally see only the rendered page, the source code often contains valuable information about the application's structure, technologies, and hidden functionality.

---

## Learning Objectives

- Understand the purpose of page source analysis
- Learn how to inspect HTML source code
- Identify sensitive information exposed in source files
- Discover hidden resources and application components
- Improve manual reconnaissance techniques

---

## Viewing the Source Code

Every web page is built using HTML, which the browser renders into the interface users interact with.

Viewing the page source reveals the original document received from the server before any client-side processing occurs.

Most browsers allow access through:

- Right-click → View Page Source
- `Ctrl + U`

---

## Information Found in HTML

The page source may reveal details that are not immediately visible on the rendered page.

Examples include:

- HTML comments
- Hidden form fields
- Internal links
- Image locations
- JavaScript files
- CSS files
- Metadata
- Page structure

Reviewing the source provides a deeper understanding of how the application is built.

---

## HTML Comments

Developers sometimes leave comments inside the source code.

Examples may include:

- Development notes
- TODO items
- Disabled functionality
- Internal URLs
- Testing information

Although comments are ignored by the browser, they remain visible to anyone viewing the source.

---

## Hidden Resources

The source code often references additional resources that are not immediately obvious.

Common examples include:

- JavaScript files
- CSS files
- Images
- Fonts
- External libraries
- API endpoints

These resources can provide useful information during reconnaissance.

---

## Forms and Input Fields

HTML forms expose how user input is collected.

Inspect:

- Form actions
- Input names
- Hidden fields
- Submission methods
- Validation attributes

Understanding form structure is useful before testing authentication or input validation.

---

## Why Source Code Matters

Analysing the page source helps identify information that may not appear in the browser interface.

Potential discoveries include:

- Hidden functionality
- Developer comments
- Internal resources
- Application structure
- Client-side logic

Even small pieces of information can assist later stages of a penetration test.

---

## Skills Practiced

- HTML source analysis
- Manual reconnaissance
- Information gathering
- Hidden resource discovery
- Client-side inspection

---

## Key Takeaways

- Always review the page source during reconnaissance.
- HTML often exposes information not visible in the rendered page.
- Comments and hidden resources may reveal useful intelligence.
- Source code analysis improves understanding of the application's structure.
- Manual inspection is an essential web application testing skill.