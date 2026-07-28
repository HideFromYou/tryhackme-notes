# Battering Ram

## Overview

The **Battering Ram** attack type applies the same payload to every selected position within an HTTP request simultaneously. Unlike the Sniper attack, which tests one position at a time, Battering Ram modifies all selected positions using a single payload from one payload set before moving on to the next payload.

This attack type is useful when multiple parameters are expected to contain the same value during testing.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how the Battering Ram attack type works
- Explain how payloads are applied across multiple positions
- Identify scenarios where Battering Ram is appropriate
- Compare Battering Ram with the Sniper attack type

---

## Main Content

### How Battering Ram Works

Battering Ram uses **one payload set**.

For each request, Intruder selects a single payload and inserts that same value into every defined position simultaneously. Once the request is sent, the next payload from the list is applied to all positions.

This process continues until every payload has been tested.

---

### Request Generation

The number of generated requests is determined solely by the number of payloads in the payload set.

Each payload produces exactly one request, regardless of how many positions have been selected.

---

### Common Use Cases

Battering Ram is commonly used when:

- Multiple parameters are expected to contain identical values
- The same credential must be supplied in different fields
- Consistent input is required across several request parameters
- Testing application behaviour with synchronized values

---

### Advantages

- Simple configuration
- Generates fewer requests than other multi-position attack types
- Maintains identical input across all selected positions
- Useful for specialised authentication and validation testing

---

## Skills Practiced

- Battering Ram Configuration
- Multi-Position Testing
- Payload Management
- HTTP Request Automation
- Response Analysis

---

## Key Takeaways

- Battering Ram uses a single payload set.
- The same payload is inserted into every selected position simultaneously.
- Each payload generates one HTTP request.
- It is best suited for scenarios where multiple parameters should contain identical values.
- Understanding Battering Ram helps in selecting the most efficient attack strategy for specific testing objectives.