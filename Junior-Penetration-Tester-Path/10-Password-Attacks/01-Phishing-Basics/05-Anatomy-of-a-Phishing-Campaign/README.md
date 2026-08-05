# Anatomy of a Phishing Campaign

## Overview

A successful phishing campaign is far more than sending malicious emails. Professional phishing engagements follow a structured lifecycle that includes planning, reconnaissance, scenario development, execution, and reporting. Each phase is designed to ensure the campaign is realistic, ethical, measurable, and aligned with the client's objectives.

In penetration testing, phishing simulations are conducted to assess an organization's resilience against social engineering attacks while remaining within agreed legal and technical boundaries.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the lifecycle of a phishing campaign
- Explain each phase of a phishing engagement
- Recognize the importance of planning and legal authorization
- Identify common phishing campaign metrics
- Produce meaningful recommendations based on campaign results

---

## Main Content

### Planning & Scoping

Every phishing engagement begins by defining the campaign's objectives.

Planning includes:

- Agreeing on the campaign scope
- Identifying target user groups
- Defining success metrics
- Establishing campaign timing
- Recording Rules of Engagement (RoE)
- Defining kill switches and emergency contacts
- Obtaining legal authorization

Proper planning ensures the campaign remains safe, ethical, and controlled.

---

### Reconnaissance

Reconnaissance relies exclusively on **Open Source Intelligence (OSINT)** to create believable phishing scenarios.

Typical information sources include:

- Company websites
- Press releases
- LinkedIn profiles
- Public social media
- Recent company news

The objective is to gather sufficient context while remaining within the agreed scope.

---

### Scenario & Payload Development

Information gathered during reconnaissance is used to create realistic phishing scenarios.

Common pretexts include:

- IT notifications
- HR announcements
- Invoice reminders
- Company policy updates

Safe payloads may include:

- Tracking links
- Fake login pages
- Branded landing pages
- Benign attachments

Malware and real credential collection should be avoided during ethical assessments.

---

### Exploitation & Post-Exploitation

The campaign is executed according to the agreed plan while monitoring user interactions.

Common metrics include:

- Email opens
- Link clicks
- Simulated credential submissions
- User reports

Campaigns should always include:

- A kill switch
- Continuous monitoring
- An escalation procedure
- Authorized tooling such as GoPhish

If unexpected behavior occurs, the campaign should be paused immediately.

---

### Reporting & Debriefing

After the campaign concludes, the collected data is analyzed to identify organizational weaknesses.

Reports should focus on:

- Click rates
- Credential submission attempts
- Reporting behavior
- Departmental trends
- Practical recommendations

Reports should avoid identifying individual employees and instead prioritize organizational improvements.

---

### Common Phishing Metrics

Several metrics help evaluate campaign effectiveness:

| Metric | Purpose |
|----------|---------|
| **Open Rate** | Percentage of users who opened the email |
| **Click Rate** | Percentage of users who clicked a phishing link |
| **Credential Entry Rate** | Percentage of users who attempted to submit credentials |
| **Attachment Detonation Rate** | Percentage of users who opened or executed an attachment |
| **Reporting Rate** | Percentage of users who reported the phishing email |

These measurements allow penetration testers to assess user awareness and recommend targeted improvements.

---

### Improving Security

Based on campaign results, organizations may improve their security by:

- Delivering targeted security awareness training
- Deploying phishing-resistant MFA
- Configuring SPF, DKIM, and DMARC
- Improving email reporting processes
- Scheduling future phishing simulations

Continuous testing allows organizations to measure progress over time.

---

## Skills Practiced

- Phishing Campaign Planning
- OSINT
- Social Engineering
- Security Awareness
- Security Reporting
- Penetration Testing

---

## Key Takeaways

- Professional phishing campaigns follow a structured lifecycle from planning through reporting.
- Proper scoping, authorization, and Rules of Engagement are essential before conducting any phishing exercise.
- OSINT enables realistic phishing scenarios while remaining ethical and within scope.
- Campaign success is measured using metrics such as open rates, click rates, credential entry rates, attachment detonation rates, and reporting rates.
- The primary objective of phishing assessments is to improve organizational security through actionable recommendations rather than simply measuring user failures.