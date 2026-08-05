# The Social Engineering Toolkit (SET)

## Overview

The **Social Engineering Toolkit (SET)** is an open-source framework designed to help penetration testers simulate realistic social engineering attacks. It automates many stages of a phishing engagement, including creating phishing websites, harvesting credentials, generating payloads, and managing phishing campaigns.

In this practical exercise, SET is used to perform a **spear phishing attack** against a simulated target by creating a credential harvesting website, sending a spoofed phishing email, and capturing submitted credentials in a controlled environment.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the purpose of the Social Engineering Toolkit
- Configure a Credential Harvester attack
- Import a custom phishing website into SET
- Perform basic email spoofing
- Capture credentials during a phishing simulation
- Understand the workflow of a spear phishing engagement

---

## Main Content

### Scenario

The engagement begins after completing an OSINT investigation.

Information gathered about the target organization includes:

- Target user: **Bob**, Head of Finance
- Email address discovered through LinkedIn
- Strict password policy
- Email security controls in place

The objective is to obtain Bob's credentials by performing a spear phishing attack.

---

### Launching SET

The Social Engineering Toolkit is started from the attack machine.

The exercise navigates through the following SET modules:

- Social-Engineering Attacks
- Website Attack Vectors
- Credential Harvester Attack Method
- Custom Import

This workflow prepares a phishing website capable of collecting submitted credentials.

---

### Credential Harvester

Instead of cloning a live website, the practical imports a custom HTML page.

Configuration includes:

- Importing `index.html`
- Configuring the POST-back IP address
- Running the Credential Harvester on port 80

Once started, SET waits for victims to submit credentials through the phishing page.

---

### Typosquatting

The phishing website uses a **typosquatted domain**:

- Legitimate: `tryaccounting.thm`
- Phishing: `tryacounting.thm`

The missing letter makes the fake domain appear legitimate while directing users to the attacker's server.

---

### Email Delivery

The phishing email is sent using the Rainloop webmail client.

To improve credibility, the sender address is changed to:

- `support@tryaccounting.thm`

The phishing email uses a password expiration pretext requesting Bob to visit the phishing website and update his password.

Basic sender spoofing helps bypass simple email filtering mechanisms.

---

### Capturing Credentials

When the victim submits credentials through the phishing page, SET records the submitted values in real time.

The terminal displays:

- Username field
- Password field

This confirms the successful execution of the spear phishing campaign.

---

### Ethical Use

The Social Engineering Toolkit should only be used:

- During authorized penetration tests
- Within the agreed Rules of Engagement
- In controlled lab environments
- With explicit written permission

Its purpose is to evaluate organizational resilience against social engineering attacks rather than compromise real users.

---

## Skills Practiced

- Social Engineering Toolkit (SET)
- Spear Phishing
- Credential Harvesting
- Email Spoofing
- Typosquatting
- Social Engineering
- Penetration Testing

---

## Key Takeaways

- The Social Engineering Toolkit automates many stages of phishing engagements.
- Credential Harvester creates phishing websites capable of collecting submitted credentials.
- Typosquatted domains significantly increase the credibility of phishing campaigns.
- Basic email spoofing helps phishing emails appear legitimate.
- Ethical phishing engagements must always be authorized, controlled, and conducted within the agreed Rules of Engagement.