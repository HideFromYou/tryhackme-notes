# Sniper

## Overview

The **Sniper** attack type is the default mode in Burp Suite Intruder and is commonly used for testing a single parameter at a time. It inserts each payload into one selected position while keeping all other positions unchanged, allowing testers to isolate and analyse the effect of individual inputs.

This approach is particularly useful when fuzzing parameters or performing targeted input validation during web application assessments.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how the Sniper attack type works
- Explain how payloads are applied to request positions
- Identify scenarios where Sniper is the most appropriate attack type
- Understand how the number of generated requests is determined

---

## Main Content

### How Sniper Works

The Sniper attack type uses a **single payload set**.

If multiple positions are selected, Intruder tests each position independently by inserting every payload into one position at a time while leaving the remaining positions unchanged.

This allows each parameter to be evaluated individually without affecting the others.

---

### Request Generation

The total number of requests depends on:

- The number of selected positions
- The number of payloads in the payload set

Each payload is tested against every selected position, producing a predictable sequence of requests.

---

### Common Use Cases

Sniper is commonly used for:

- Parameter fuzzing
- Input validation testing
- Identifier discovery
- Authentication testing
- API parameter analysis

Because only one parameter changes at a time, identifying the source of different server responses becomes much easier.

---

### Advantages

- Simple to configure
- Easy to analyse results
- Ideal for single-parameter testing
- Generates predictable request sequences

---

## Skills Practiced

- Sniper Attack Configuration
- Payload Management
- Position Selection
- HTTP Request Automation
- Response Analysis

---

## Key Takeaways

- Sniper is Burp Suite Intruder's default attack type.
- It accepts a single payload set.
- Only one selected position is modified during each request.
- Every payload is tested against every selected position individually.
- Sniper is well suited for focused testing and parameter fuzzing.