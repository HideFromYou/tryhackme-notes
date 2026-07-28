# Cluster Bomb

## Overview

The **Cluster Bomb** attack type is the most comprehensive attack mode available in Burp Suite Intruder. It supports multiple payload sets and generates every possible combination of payloads across the selected positions.

Unlike Pitchfork, which processes payload sets in parallel, Cluster Bomb exhaustively tests all combinations, making it particularly useful when the relationship between input values is unknown.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand how the Cluster Bomb attack type works
- Configure multiple payload sets
- Explain how payload combinations are generated
- Identify scenarios where Cluster Bomb is the most suitable attack type
- Understand the impact of large payload sets on the number of generated requests

---

## Main Content

### How Cluster Bomb Works

Cluster Bomb allows each selected position to use its own payload set.

Instead of processing payloads in parallel, Intruder generates every possible combination between the payload sets. This ensures that all value combinations are tested during the attack.

As the number of payloads or positions increases, the total number of generated requests grows rapidly.

---

### Request Generation

The total number of requests is calculated by multiplying the number of payloads in each payload set.

For example, if two payload sets contain 10 and 20 entries respectively, Intruder generates **200 unique requests**.

Because of this exponential growth, Cluster Bomb attacks can become resource-intensive when large payload sets are used.

---

### Common Use Cases

Cluster Bomb is commonly used for:

- Username and password testing
- Multi-parameter brute-force attacks
- Testing unknown parameter relationships
- Exhaustive input combination testing

---

### Advantages

- Supports multiple payload sets
- Tests every possible payload combination
- Provides comprehensive coverage
- Effective when relationships between parameters are unknown

---

### Considerations

Because Cluster Bomb generates every possible combination, it can produce a very large number of requests. Selecting appropriate payload lists helps reduce unnecessary traffic and improves testing efficiency.

---

## Skills Practiced

- Cluster Bomb Configuration
- Multiple Payload Sets
- Payload Combination Testing
- HTTP Request Automation
- Response Analysis

---

## Key Takeaways

- Cluster Bomb uses multiple payload sets.
- Every possible payload combination is generated and tested.
- The number of requests equals the product of all payload set sizes.
- It provides the most exhaustive testing of all Intruder attack types.
- Cluster Bomb is ideal when parameter relationships are unknown and complete coverage is required.