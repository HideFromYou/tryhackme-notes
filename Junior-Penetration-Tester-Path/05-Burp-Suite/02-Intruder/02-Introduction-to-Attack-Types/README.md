# Introduction to Attack Types

## Overview

Burp Suite Intruder provides four different attack types, each designed for a specific testing scenario. While all attack types use positions and payloads, they differ in how payloads are applied to the selected positions within an HTTP request.

Choosing the appropriate attack type improves testing efficiency and ensures that requests are generated according to the assessment objective.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify the four Intruder attack types
- Understand how each attack type processes payloads
- Compare the behaviour of different attack strategies
- Choose the appropriate attack type for different testing scenarios

---

## Main Content

### Sniper

The **Sniper** attack type is the default Intruder mode. It inserts one payload at a time into each selected position while leaving all other positions unchanged.

It is well suited for testing individual parameters independently.

---

### Battering Ram

The **Battering Ram** attack type uses a single payload set and inserts the same payload into every selected position simultaneously.

This approach is useful when multiple parameters are expected to contain identical values.

---

### Pitchfork

The **Pitchfork** attack type allows multiple payload sets to be used at the same time.

Each selected position receives values from its own payload set, and payloads are processed in parallel.

---

### Cluster Bomb

The **Cluster Bomb** attack type also supports multiple payload sets but generates every possible combination between them.

This provides comprehensive coverage when testing multiple parameters with independent value sets.

---

### Comparing Attack Types

| Attack Type | Payload Sets | Payload Behaviour |
|--------------|--------------|-------------------|
| Sniper | 1 | Tests one position at a time |
| Battering Ram | 1 | Uses the same payload in every position |
| Pitchfork | Multiple | Processes payload sets in parallel |
| Cluster Bomb | Multiple | Tests every possible payload combination |

---

## Skills Practiced

- Intruder Configuration
- Attack Type Selection
- Payload Strategy
- HTTP Request Automation
- Web Application Testing

---

## Key Takeaways

- Burp Suite Intruder offers four attack types for different testing scenarios.
- Each attack type applies payloads differently.
- Understanding these differences helps select the most appropriate testing strategy.
- Choosing the correct attack type improves both efficiency and testing accuracy.