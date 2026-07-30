# SSRF Practical

## Overview

This practical exercise applies the concepts introduced throughout the SSRF room in a controlled environment. Rather than focusing on theory, the objective is to recognise vulnerable functionality, analyse how server-side requests are generated, and understand how SSRF can be identified during a web application security assessment.

The lab reinforces the importance of carefully evaluating application features that retrieve resources on behalf of users while maintaining a structured and methodical testing approach.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Apply SSRF concepts in a practical environment
- Identify functionality that performs server-side requests
- Analyse how user input influences outbound requests
- Evaluate application behaviour during SSRF testing
- Reinforce secure testing methodology for web applications

---

## Main Content

### Identifying the Attack Surface

The first step in the practical exercise is identifying features that cause the application to retrieve resources on behalf of the user.

Typical functionality includes:

- Resource fetching
- API integrations
- File retrieval
- URL previews
- Image processing

Recognising these features is essential for identifying potential SSRF vulnerabilities.

---

### Analysing Request Behaviour

During testing, attention should be given to how the application constructs outbound requests.

Important observations include:

- User-controlled parameters
- Destination validation
- Server responses
- Error handling
- Network behaviour

These observations help determine whether user input can influence server-side communication.

---

### Evaluating Security Controls

Practical assessments should also examine whether the application implements appropriate protections.

Areas to evaluate include:

- URL validation
- Destination restrictions
- Request filtering
- Access controls
- Error handling consistency

Properly implemented controls significantly reduce SSRF risk.

---

### Reinforcing a Security Methodology

Successful SSRF assessments follow a consistent process:

- Identify server-side request functionality
- Analyse user-controlled input
- Observe application behaviour
- Evaluate defensive mechanisms
- Document findings responsibly

Following a structured methodology improves both accuracy and repeatability during security testing.

---

## Skills Practiced

- SSRF Assessment
- HTTP Request Analysis
- Attack Surface Identification
- Web Application Security
- Security Testing Methodology

---

## Key Takeaways

- Practical exercises reinforce the concepts introduced throughout the SSRF room.
- Server-side request functionality should always be considered a potential attack surface.
- Careful observation of application behaviour helps identify SSRF vulnerabilities.
- Secure testing relies on methodology, documentation, and responsible analysis rather than trial and error.
- Understanding both offensive concepts and defensive controls strengthens web application security assessments.