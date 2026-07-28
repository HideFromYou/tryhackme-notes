# Pitchfork

## Overview

The **Pitchfork** attack type allows Burp Suite Intruder to use multiple payload sets simultaneously. Each selected position is assigned its own payload set, and Intruder inserts payloads from each set into their corresponding positions during every request.

Unlike Battering Ram, where the same payload is reused across all positions, Pitchfork enables different values to be tested together in a synchronized manner.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how the Pitchfork attack type works
- Configure multiple payload sets
- Explain how payloads are matched to individual positions
- Identify scenarios where Pitchfork is the most appropriate attack type

---

## Main Content

### How Pitchfork Works

Pitchfork uses **multiple payload sets**, with one payload set assigned to each selected position.

For every request, Intruder takes the next value from each payload set and inserts it into its corresponding position. All payload sets advance together, meaning the first payload from each set is used in the first request, the second payloads in the second request, and so on.

This process continues until one of the payload sets is exhausted.

---

### Request Generation

The total number of generated requests depends on the size of the smallest payload set.

Because all payload sets progress in parallel, the attack stops once there are no remaining payloads in one of the sets.

---

### Common Use Cases

Pitchfork is commonly used for:

- Testing paired credentials
- Multi-parameter authentication requests
- Requests requiring synchronized input values
- Parameter testing where values have predefined relationships

---

### Advantages

- Supports multiple payload sets
- Maintains relationships between corresponding payload values
- Efficient for synchronized testing
- Generates fewer requests than Cluster Bomb

---

## Skills Practiced

- Pitchfork Configuration
- Multiple Payload Sets
- Multi-Parameter Testing
- HTTP Request Automation
- Response Analysis

---

## Key Takeaways

- Pitchfork uses multiple payload sets simultaneously.
- Each selected position receives values from its own payload set.
- Payload sets advance together in parallel.
- The attack ends when the shortest payload set is exhausted.
- Pitchfork is ideal when payload values have a one-to-one relationship across multiple parameters.