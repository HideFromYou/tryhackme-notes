# Practical Example

## Overview

This lesson demonstrates how Burp Suite Intruder can be applied in a realistic testing scenario. It focuses on configuring an attack, selecting the appropriate positions and payloads, launching the attack, and analysing the responses to identify meaningful results.

Rather than introducing new attack types, this exercise reinforces the concepts learned in previous lessons by applying them in a practical workflow.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Configure an Intruder attack from an intercepted request
- Select appropriate positions for testing
- Configure payloads for a specific objective
- Launch an Intruder attack
- Analyse response data to identify interesting results

---

## Main Content

### Preparing the Request

The first step is selecting an HTTP request that will serve as the template for the attack. Appropriate positions are identified based on the parameters being tested.

---

### Configuring the Attack

Once the positions have been defined, payloads are configured according to the testing objective. Selecting the correct attack type ensures that payloads are applied in the desired manner.

---

### Launching the Attack

Intruder automatically generates and sends multiple HTTP requests using the configured payloads and positions.

Each request follows the behaviour defined by the selected attack type.

---

### Analysing Responses

After the attack completes, the generated responses are reviewed to identify:

- Different status codes
- Response length variations
- Error messages
- Successful responses
- Other behavioural differences

Careful analysis helps distinguish normal application behaviour from potentially interesting results.

---

## Skills Practiced

- Intruder Configuration
- Payload Selection
- Position Identification
- HTTP Request Automation
- Response Analysis

---

## Key Takeaways

- Practical testing combines positions, payloads, and attack types into a complete workflow.
- Selecting the correct attack configuration improves testing efficiency.
- Response analysis is as important as the attack itself.
- Differences in server responses often indicate areas requiring further investigation.
- Intruder streamlines repetitive testing while allowing testers to focus on analysing results.