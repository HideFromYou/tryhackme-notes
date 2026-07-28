# Challenge

## Overview

This lesson provides a hands-on challenge designed to strengthen the skills developed throughout the Repeater module. By modifying HTTP requests and carefully observing server responses, testers learn how small input changes can reveal unexpected application behaviour.

The challenge encourages a methodical approach to manual testing and demonstrates the value of experimenting with request parameters in a controlled environment.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Apply the Repeater workflow in a practical challenge
- Modify request parameters manually
- Observe how applications handle unexpected input
- Analyse server responses for abnormal behaviour
- Develop a structured methodology for manual testing

---

## Main Content

### Understanding the Target

Before modifying requests, it is important to understand how the application processes user input and validates request parameters.

Carefully reviewing the request structure helps determine which values are suitable for testing.

---

### Modifying Parameters

Repeater allows individual request components to be edited without affecting the rest of the request.

Typical areas for testing include:

- URL paths
- Query parameters
- Form values
- Headers
- Cookies

Changing one value at a time makes it easier to identify the cause of any behavioural differences.

---

### Sending and Reviewing Requests

Each modified request is sent directly from Repeater, allowing immediate observation of the application's response.

Responses should be reviewed for changes such as:

- HTTP status codes
- Error messages
- Redirect behaviour
- Response size
- Content differences

These observations provide valuable insight into how the application validates input.

---

## Skills Practiced

- Manual Request Testing
- Parameter Manipulation
- Response Analysis
- Input Validation Testing
- Burp Suite Repeater Workflow

---

## Key Takeaways

- Manual request modification helps identify how applications process user input.
- Repeater enables rapid testing without repeated browser interaction.
- Careful response analysis is essential for understanding application behaviour.
- A structured testing methodology improves both efficiency and accuracy during security assessments.