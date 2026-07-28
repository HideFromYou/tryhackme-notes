# Repeater: Basic Usage & Analysis Toolbar

## Overview

Burp Suite Repeater is a manual testing tool that enables security professionals to modify and resend HTTP requests while immediately viewing the corresponding server responses. Unlike automated modules, Repeater focuses on interactive testing, allowing individual requests to be refined and analysed in real time.

This lesson introduces the Repeater interface, demonstrates its basic workflow, and explains how the Analysis Toolbar assists in interpreting server responses.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the purpose of Burp Suite Repeater
- Send intercepted requests to Repeater
- Modify HTTP requests manually
- Analyse server responses
- Use the Analysis Toolbar to inspect response details

---

## Main Content

### What is Repeater?

Repeater allows a previously captured HTTP request to be edited and resent multiple times without interacting with the web application through a browser.

This provides a controlled environment for testing how small modifications affect the application's behaviour.

---

### Basic Workflow

A typical Repeater workflow consists of:

1. Capturing a request.
2. Sending it to Repeater.
3. Modifying one or more request components.
4. Resending the request.
5. Analysing the server's response.

This process can be repeated as many times as needed.

---

### Request Modification

Repeater allows nearly every part of an HTTP request to be edited, including:

- URL paths
- Parameters
- Headers
- Cookies
- Request body
- HTTP methods

This flexibility makes Repeater one of the most valuable tools for manual web application testing.

---

### Analysis Toolbar

The Analysis Toolbar provides useful information about server responses, helping testers quickly identify important characteristics.

Typical observations include:

- HTTP status codes
- Response headers
- Response size
- Content type
- Other response metadata

These details assist in understanding how the application reacts to modified requests.

---

## Skills Practiced

- Manual Request Testing
- HTTP Request Editing
- Response Analysis
- Header Inspection
- Burp Suite Repeater Workflow

---

## Key Takeaways

- Repeater enables manual modification and replay of HTTP requests.
- It provides immediate feedback after each request is sent.
- The Analysis Toolbar simplifies response inspection.
- Repeater is ideal for validating application behaviour through iterative testing.
- Careful response analysis is essential during manual web application security assessments.