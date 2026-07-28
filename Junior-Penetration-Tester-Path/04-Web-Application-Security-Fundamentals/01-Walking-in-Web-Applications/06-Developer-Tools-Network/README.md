# Developer Tools - Network

## Overview

The Network tab is one of the most valuable browser developer tools during web application testing. It provides visibility into every HTTP and HTTPS request exchanged between the browser and the web server, allowing penetration testers to analyse how an application communicates, loads resources, and exchanges data.

---

## Learning Objectives

- Understand the purpose of the Network tab
- Analyse HTTP requests and responses
- Monitor resources loaded by a web application
- Identify communication between the client and the server
- Understand how web applications exchange data

---

## What is the Network Tab?

The Network tab records every request made by the browser while interacting with a website.

This includes requests for:

- HTML pages
- CSS stylesheets
- JavaScript files
- Images
- Fonts
- API requests
- Videos
- Other web resources

Refreshing the page immediately displays all communication between the client and the server.

---

## HTTP Requests

Each network request contains useful information about how the application operates.

Common details include:

- Request URL
- HTTP Method
- Status Code
- Request Headers
- Response Headers
- Query Parameters
- Request Body
- Response Body

Reviewing these values helps build a complete understanding of application behaviour.

---

## HTTP Methods

Common HTTP methods include:

| Method | Purpose |
|---------|----------|
| GET | Retrieve data from the server |
| POST | Submit data to the server |
| PUT | Update existing resources |
| PATCH | Modify part of a resource |
| DELETE | Remove a resource |

Understanding which methods are used is important during security assessments.

---

## Response Codes

The Network tab also displays HTTP status codes returned by the server.

Common examples include:

- **200 OK**
- **301 Moved Permanently**
- **302 Found**
- **403 Forbidden**
- **404 Not Found**
- **500 Internal Server Error**

Status codes provide insight into server behaviour and application logic.

---

## Analysing Requests

While navigating a website, observe:

- Which requests are generated
- Which parameters are sent
- How authentication is handled
- Which APIs are used
- How data is transferred

Unexpected requests may reveal hidden functionality or additional attack surfaces.

---

## Filtering Traffic

Developer Tools allow requests to be filtered by resource type, making analysis easier.

Examples include:

- Documents
- Fetch/XHR
- JavaScript
- CSS
- Images
- Media
- Fonts

Filtering helps isolate the traffic relevant to a particular action.

---

## Security Considerations

The Network tab can reveal:

- API endpoints
- Hidden parameters
- Session identifiers
- Authentication requests
- File uploads
- Download locations

Understanding network traffic is essential before attempting more advanced testing.

---

## Skills Practiced

- HTTP traffic analysis
- Request and response inspection
- Network monitoring
- Client-server communication analysis
- Browser Developer Tools usage

---

## Key Takeaways

- The Network tab records every request made by the browser.
- HTTP requests reveal how applications communicate with servers.
- Analysing network traffic improves reconnaissance.
- API endpoints and parameters are often discovered through request analysis.
- Understanding web traffic is fundamental to web application security testing.