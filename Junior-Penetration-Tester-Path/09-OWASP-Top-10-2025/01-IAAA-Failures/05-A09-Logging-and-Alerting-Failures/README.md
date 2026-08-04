# A09 - Logging & Alerting Failures

## Overview

**Logging & Alerting Failures** occur when applications fail to properly record, store, or alert on security-related events. Without reliable logging, security teams cannot detect attacks, investigate incidents, or determine what actions an attacker performed after compromising an account.

Logging is a critical component of **Accountability** within the **IAAA** model because it provides evidence of **who performed an action, when it occurred, and from where**. Missing authentication logs, inadequate monitoring, or the absence of alerts can significantly delay incident detection and response. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand what Logging & Alerting Failures are
- Explain why logging supports accountability
- Identify common logging weaknesses
- Recognize the importance of security monitoring
- Apply secure logging best practices

---

## Main Content

### What are Logging & Alerting Failures?

Logging & Alerting Failures occur when security-relevant events are not properly recorded or monitored.

Without sufficient logging, defenders cannot:

- Detect attacks
- Investigate incidents
- Identify compromised accounts
- Reconstruct attacker activity :contentReference[oaicite:1]{index=1}

---

### Accountability

Within the **IAAA** model, **Accountability** ensures that user actions can be traced.

Effective logging should answer:

- Who performed the action?
- What action occurred?
- When did it happen?
- From which IP address or location?

Without this information, incident response becomes significantly more difficult. :contentReference[oaicite:2]{index=2}

---

### Common Logging Weaknesses

The room identifies several common failures:

- Missing authentication logs
- Incomplete or vague error messages
- No alerts for brute-force attacks
- No alerts for privilege changes
- Short log retention
- Logs stored where attackers can modify or delete them

Each weakness reduces the defender's visibility into malicious activity. :contentReference[oaicite:3]{index=3}

---

### Why Monitoring Matters

Logging alone is not enough.

Applications should also generate alerts for suspicious activity such as:

- Multiple failed login attempts
- Brute-force attacks
- Privilege escalation
- Administrative actions
- Unusual authentication behavior

Timely alerting allows defenders to respond before attackers achieve their objectives. :contentReference[oaicite:4]{index=4}

---

### Secure Logging Practices

Applications should:

- Log authentication successes and failures.
- Record administrative actions.
- Monitor privilege changes.
- Store logs securely.
- Retain logs for forensic investigations.
- Generate alerts for suspicious behavior.

Strong logging improves both detection and incident response capabilities. :contentReference[oaicite:5]{index=5}

---

## Skills Practiced

- Security Logging
- Incident Investigation
- Security Monitoring
- Accountability
- Web Application Security
- Incident Response

---

## Key Takeaways

- Logging & Alerting Failures reduce an organization's ability to detect and investigate attacks.
- Accountability depends on recording who performed each action, when it occurred, and from where.
- Missing logs, poor retention, and absent alerts significantly weaken security monitoring.
- Logging should be combined with real-time alerting for suspicious activity.
- Effective monitoring is essential for detecting attacks, supporting forensic investigations, and improving incident response. :contentReference[oaicite:6]{index=6}