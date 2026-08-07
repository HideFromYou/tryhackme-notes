# 07-Reading-a-CIS-Benchmark/README.md

# Reading a CIS Benchmark

## Overview

A CIS Benchmark is more than a list of recommendations—it is a structured security document explaining how systems should be configured and why each recommendation matters.

Penetration testers use CIS Benchmarks to identify deviations that may lead to privilege escalation or other security weaknesses.

---

## Learning Objectives

- Read CIS recommendations
- Interpret benchmark structure
- Understand recommendation rationale
- Identify exploitable deviations

---

## Typical Benchmark Entry

A recommendation normally contains:

- Recommendation number
- Title
- Description
- Rationale
- Audit procedure
- Remediation guidance
- References

---

## Example Structure

```text
Recommendation
      ↓
Rationale
      ↓
Audit
      ↓
Remediation
```

---

## Offensive Perspective

When reading a benchmark, ask:

- Is this recommendation implemented?
- If not, does it introduce risk?
- Can the deviation be abused?
- Does it contribute to privilege escalation?

---

## Why Benchmarks Matter

Benchmarks help:

- Standardise reviews
- Justify findings
- Explain security impact
- Recommend remediation

They also improve communication with system administrators.

---

## Skills Practiced

- CIS Benchmark Analysis
- Security Reviews
- Configuration Assessment

---

## Key Takeaways

- CIS Benchmarks provide structured security guidance.
- Every recommendation includes both technical and operational context.
- Deviations from benchmark recommendations often become valuable penetration testing findings.