# Developer Tools - Inspector

## Overview

The Inspector is one of the most useful browser developer tools for web application reconnaissance. It allows penetration testers to examine the Document Object Model (DOM), inspect HTML and CSS, and understand how web pages are structured. This provides valuable insight into client-side functionality and exposed application components.

---

## Learning Objectives

- Understand the purpose of the Inspector tool
- Learn how to inspect HTML elements
- Explore the Document Object Model (DOM)
- Identify hidden client-side components
- Understand how browsers render web pages

---

## What is the Inspector?

The Inspector displays the live HTML structure of a web page after it has been rendered by the browser.

Unlike viewing the page source, the Inspector reflects the current state of the page, including any modifications made dynamically through JavaScript.

---

## Inspecting HTML Elements

Selecting an element in the Inspector highlights its position on the page and displays its associated HTML.

Useful information includes:

- Element type
- Attributes
- IDs
- CSS classes
- Nested elements
- Form components

Understanding the page structure makes it easier to identify potential targets for testing.

---

## Understanding the DOM

The Document Object Model (DOM) represents the structure of a web page as a hierarchy of elements.

Common elements include:

- `<html>`
- `<head>`
- `<body>`
- `<div>`
- `<form>`
- `<input>`
- `<button>`
- `<img>`

Modern web applications frequently modify the DOM dynamically using JavaScript.

---

## CSS Inspection

The Inspector also displays the CSS rules applied to each element.

Reviewing styles can help identify:

- Hidden elements
- Disabled components
- Responsive layouts
- Dynamically applied classes

Although CSS itself is not usually vulnerable, it often reveals application behaviour.

---

## Editing the DOM

Developer Tools allow temporary modifications to the page directly within the browser.

Examples include:

- Editing text
- Modifying HTML elements
- Changing CSS properties
- Revealing hidden elements

These changes affect only the local browser session and do not modify the server.

---

## Security Considerations

The Inspector is useful for identifying:

- Hidden input fields
- Disabled form elements
- Client-side validation
- Exposed application logic
- Interesting HTML attributes

Client-side restrictions should never be trusted without proper server-side validation.

---

## Skills Practiced

- DOM inspection
- HTML analysis
- CSS inspection
- Client-side reconnaissance
- Browser Developer Tools usage

---

## Key Takeaways

- The Inspector provides a live view of a web page's structure.
- The DOM may differ from the original page source.
- Hidden elements can often be discovered through inspection.
- Client-side controls should not be considered security mechanisms.
- Understanding page structure improves web application testing.