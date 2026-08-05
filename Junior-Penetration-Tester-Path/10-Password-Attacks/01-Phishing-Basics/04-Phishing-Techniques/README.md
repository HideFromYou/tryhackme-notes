# Phishing Techniques

## Overview

Phishing campaigns combine **social engineering** with technical manipulation to persuade victims to interact with attacker-controlled content. These techniques are designed to make malicious emails, links, or websites appear legitimate while increasing the likelihood that users will click a link, submit credentials, or execute malicious files.

This lesson explores common phishing techniques used during penetration tests, including URL manipulation, email spoofing, credential harvesting, payload delivery, and the tools commonly used to build phishing campaigns. :contentReference[oaicite:0]{index=0}

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify common phishing techniques
- Explain how attackers manipulate URLs and email messages
- Understand credential harvesting attacks
- Describe common payload delivery mechanisms
- Recognize tools used during phishing engagements

---

## Main Content

### URL and Domain Manipulation

One of the primary objectives of a phishing campaign is to convince victims to visit an attacker-controlled website.

Common techniques include:

#### URL Masking

A malicious URL is hidden behind a legitimate-looking hyperlink.

Example:

- Displayed: `https://tryhackme.com`
- Actual destination: `http://phisher.thm`

---

#### Homograph Attacks

Homograph attacks exploit visually similar characters within domain names.

Examples include:

- Replacing **o** with **0**
- Using Unicode or Cyrillic characters that resemble Latin letters

A fake domain may appear almost identical to a legitimate website.

---

#### Typosquatting

Attackers register domains that closely resemble legitimate ones and rely on users making typing mistakes.

Example:

- `tryhackme.com`
- `tryhacme.com`

These domains are commonly used for phishing pages or malware delivery. :contentReference[oaicite:1]{index=1}

---

### Email Spoofing

Email spoofing attempts to impersonate trusted senders by modifying email headers or display names.

Common techniques include:

- Spoofing the **From** address
- Display name spoofing
- Using lookalike domains

Examples:

- `support@tryaccounting.thm`
- `support@tryaccounting-security.thm`

Many email clients display only the sender's name, making these attacks more convincing. :contentReference[oaicite:2]{index=2}

---

### Email Authentication

Organizations reduce spoofing attacks using:

- **SPF (Sender Policy Framework)**
- **DKIM (DomainKeys Identified Mail)**
- **DMARC (Domain-based Message Authentication, Reporting and Conformance)**

These technologies help verify that emails originate from legitimate sources. :contentReference[oaicite:3]{index=3}

---

### Credential Harvesting

Credential harvesting commonly uses cloned login pages that closely resemble legitimate websites.

The process typically works as follows:

1. The victim visits a fake login page.
2. The victim enters their credentials.
3. The credentials are sent to the attacker's server.
4. The victim is redirected to the legitimate website.

Because the victim often believes they simply mistyped their password, the attack may go unnoticed. :contentReference[oaicite:4]{index=4}

---

### Payload Delivery

Phishing campaigns frequently deliver malicious documents containing macros.

Typical attack flow:

1. Victim opens a `.docm` attachment.
2. Microsoft Word requests **Enable Content**.
3. The victim enables macros.
4. A hidden VBA macro executes.
5. During a penetration test, the payload is typically replaced with a harmless beacon that confirms successful execution. :contentReference[oaicite:5]{index=5}

---

### Common Phishing Tools

The lesson introduces several popular phishing frameworks:

- **GoPhish** – Creates and manages phishing campaigns, email templates, and campaign statistics.
- **EvilNginx** – A reverse proxy used to capture credentials and session tokens, including in MFA-enabled environments.
- **Social Engineering Toolkit (SET)** – Provides tools for spear-phishing campaigns and fake login pages. :contentReference[oaicite:6]{index=6}

---

## Skills Practiced

- Phishing
- Email Spoofing
- URL Manipulation
- Credential Harvesting
- Payload Delivery
- Social Engineering
- Penetration Testing

---

## Key Takeaways

- Successful phishing campaigns combine psychological manipulation with technical deception.
- URL masking, homograph attacks, and typosquatting are common methods for directing victims to malicious websites.
- Email spoofing attempts to impersonate trusted senders and is mitigated through SPF, DKIM, and DMARC.
- Credential harvesting commonly relies on cloned login pages that capture user credentials.
- Tools such as GoPhish, EvilNginx, and SET help penetration testers build realistic phishing simulations. :contentReference[oaicite:7]{index=7}