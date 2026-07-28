# Practical Example

## Overview

This lesson demonstrates how Burp Suite Repeater can be used in a realistic testing scenario. By modifying an intercepted HTTP request and observing the resulting server responses, testers can better understand how an application processes user input and reacts to request changes.

The exercise reinforces the manual testing workflow introduced earlier and highlights the importance of carefully analysing responses after each modification.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Apply the Repeater workflow to a practical scenario
- Modify HTTP requests manually
- Observe how request changes affect server responses
- Analyse response differences
- Improve manual web application testing techniques

---

## Main Content

### Preparing the Request

The first step is selecting an intercepted HTTP request and forwarding it to Repeater.

This request becomes the testing template that can be modified repeatedly without interacting with the application through a browser.

---

### Modifying the Request

Once inside Repeater, different parts of the request can be adjusted to observe how the application responds.

Common modifications include:

- HTTP headers
- Parameters
- Cookies
- Request body values

Making one change at a time helps isolate application behaviour.

---

### Sending the Request

After each modification, the request is resent directly from Repeater.

This iterative workflow allows testers to quickly validate assumptions without generating unnecessary browser traffic.

---

### Analysing the Response

Each response should be examined for observable differences, including:

- HTTP status codes
- Response headers
- Response size
- Page content
- Application behaviour

Comparing responses after each modification helps identify meaningful changes.

---

## Skills Practiced

- Manual Request Testing
- HTTP Request Modification
- Response Analysis
- Header Manipulation
- Burp Suite Repeater Workflow

---

## Key Takeaways

- Repeater simplifies manual testing by allowing requests to be modified and resent.
- Small request changes can produce valuable insights into application behaviour.
- Analysing server responses is essential for understanding the impact of each modification.
- A structured testing approach improves both efficiency and accuracy during web application assessments.