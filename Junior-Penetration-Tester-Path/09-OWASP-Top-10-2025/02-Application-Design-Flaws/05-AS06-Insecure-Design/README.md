# AS06 - Insecure Design

## Overview

**Insecure Design** occurs when security weaknesses are built into an application's architecture, business logic, or trust model from the very beginning. Unlike implementation bugs, these vulnerabilities arise from flawed assumptions, missing threat modeling, insufficient security requirements, or poor architectural decisions.

The increasing use of **Artificial Intelligence (AI)** introduces additional design challenges. Blindly trusting AI-generated code, granting excessive permissions to AI agents, or allowing user input to influence system prompts can introduce security risks that cannot be resolved by simply patching the application later. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Insecure Design is
- Explain why design flaws differ from implementation bugs
- Recognize common insecure design patterns
- Understand how AI introduces new design risks
- Apply secure-by-design principles

---

## Main Content

### What is Insecure Design?

Insecure Design occurs when security weaknesses are introduced during the planning and architectural phases of development.

Common causes include:

- Missing threat modeling
- Weak business logic
- Incorrect trust assumptions
- Lack of security requirements
- Poor architectural decisions

Because these weaknesses are part of the application's design, they often require architectural changes rather than software patches. :contentReference[oaicite:1]{index=1}

---

### Why It Matters

Design flaws affect the entire application.

Unlike coding vulnerabilities, they cannot simply be patched after deployment because the underlying workflow, trust boundaries, or business logic remain insecure.

Correcting insecure design often requires redesigning significant parts of the system. :contentReference[oaicite:2]{index=2}

---

### Common Insecure Designs

The room highlights several common examples:

- Weak business logic
- Flawed assumptions about user behavior
- AI components with excessive authority
- Missing guardrails for LLMs and automation agents
- Test or debug functionality left enabled in production
- Missing abuse-case reviews
- Insufficient AI threat modeling :contentReference[oaicite:3]{index=3}

---

### Insecure Design in the AI Era

Modern AI systems introduce additional architectural risks.

Examples include:

- Prompt injection attacks
- Blind trust in AI-generated output
- Poisoned AI models
- Unverified third-party models
- Excessive privileges assigned to AI agents

These issues originate from system design rather than software implementation. :contentReference[oaicite:4]{index=4}

---

### Designing Secure Systems

The room recommends several secure design practices:

- Treat AI models as untrusted until verified.
- Validate model inputs and outputs.
- Separate system prompts from user content.
- Protect sensitive data.
- Require human review for high-risk AI actions.
- Apply least privilege across users, APIs, and services.
- Perform continuous threat modeling throughout the SDLC.
- Monitor systems for abuse and emerging risks. :contentReference[oaicite:5]{index=5}

---

## Skills Practiced

- Secure Architecture
- Threat Modeling
- Secure Design
- AI Security
- Business Logic Analysis
- Secure SDLC

---

## Key Takeaways

- Insecure Design originates from architectural weaknesses rather than programming mistakes.
- Design flaws often require redesign instead of software patches.
- AI systems introduce new trust, prompt injection, and model security challenges.
- Threat modeling, least privilege, and secure architectural planning significantly reduce long-term security risks.
- Building security into the design phase is more effective than attempting to add security after deployment. :contentReference[oaicite:6]{index=6}