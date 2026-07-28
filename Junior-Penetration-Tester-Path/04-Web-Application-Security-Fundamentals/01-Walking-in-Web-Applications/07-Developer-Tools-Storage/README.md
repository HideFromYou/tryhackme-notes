# Developer Tools - Storage

## Overview

The Storage tab provides visibility into the data stored by a web application inside the browser. Modern applications rely on browser storage to improve user experience by saving preferences, session information, and cached data. Understanding how this information is stored is an important part of web application reconnaissance.

---

## Learning Objectives

- Understand the purpose of browser storage
- Learn where web applications store client-side data
- Identify different storage mechanisms
- Inspect cookies and locally stored information
- Recognise security considerations related to browser storage

---

## Browser Storage

Web browsers provide several mechanisms for storing data locally.

Common storage technologies include:

- Cookies
- Local Storage
- Session Storage
- IndexedDB

Each mechanism serves a different purpose and has different security implications.

---

## Cookies

Cookies are small pieces of data stored by the browser and sent with future HTTP requests to the same website.

They are commonly used for:

- Session management
- Authentication
- User preferences
- Tracking user activity

During security testing, cookies should be reviewed to understand how the application manages user sessions.

---

## Local Storage

Local Storage allows websites to save data directly in the browser.

Characteristics include:

- Persistent storage
- Larger capacity than cookies
- Not automatically included in HTTP requests
- Accessible through JavaScript

Applications often store user preferences and non-sensitive information in Local Storage.

---

## Session Storage

Session Storage is similar to Local Storage but only exists while the browser tab remains open.

Characteristics include:

- Temporary storage
- Cleared when the tab is closed
- Isolated per browser tab
- Accessible through JavaScript

It is commonly used for temporary application data.

---

## Inspecting Stored Data

The Storage tab allows analysts to review information stored by a website.

Examples include:

- Cookie values
- Local Storage entries
- Session Storage data
- Cached application information

Reviewing stored data helps identify how the application manages client-side information.

---

## Security Considerations

Client-side storage should never contain sensitive information that could compromise user accounts or application security.

During assessments, analysts should verify whether storage contains:

- Session identifiers
- Authentication tokens
- Personally identifiable information (PII)
- Sensitive application data
- API keys
- Credentials

Sensitive information stored insecurely may increase the application's attack surface.

---

## Skills Practiced

- Browser storage analysis
- Cookie inspection
- Local Storage analysis
- Session Storage analysis
- Client-side data reconnaissance

---

## Key Takeaways

- Web applications store information locally using several browser storage mechanisms.
- Cookies are commonly used for authentication and session management.
- Local Storage and Session Storage retain client-side application data.
- Browser storage should always be reviewed during web application assessments.
- Sensitive information should never be stored insecurely on the client side.