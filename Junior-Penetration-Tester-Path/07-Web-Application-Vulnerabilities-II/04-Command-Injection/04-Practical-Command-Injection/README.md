# Practical Command Injection

## Overview

This practical lab brings together the concepts covered throughout the Command Injection room. Learners assess intentionally vulnerable web applications, identify command injection entry points, distinguish between Blind and Verbose Command Injection, and apply appropriate testing techniques to confirm whether operating system commands can be executed.

The objective is to develop a structured methodology for identifying and analysing Command Injection vulnerabilities in a controlled environment.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Identify potential Command Injection entry points
- Differentiate between Blind and Verbose Command Injection during testing
- Select appropriate payloads based on application behaviour
- Analyse how user input reaches operating system commands
- Apply a structured methodology for assessing Command Injection vulnerabilities

---

## Main Content

### Identifying Input Points

The first step is identifying every location where user input may influence operating system commands.

Common entry points include:

- URL parameters
- Form fields
- Search boxes
- POST request bodies
- HTTP headers

Any user-controlled value processed by the operating system should be considered a potential attack surface.

---

### Observing Application Behaviour

Before testing for Command Injection, observe how the application behaves under normal conditions.

Look for:

- Expected responses
- Error messages
- Execution delays
- Command output
- Changes in application behaviour

Understanding normal behaviour makes anomalies much easier to identify.

---

### Selecting Test Payloads

The choice of payload depends on the operating system and the application's response.

Typical Linux payloads include:

- `whoami`
- `ls`
- `ping`
- `sleep`

Typical Windows payloads include:

- `whoami`
- `dir`
- `ping`
- `timeout`

Time-based payloads are especially useful when testing Blind Command Injection.

---

### Building a Testing Methodology

A systematic Command Injection assessment generally follows these steps:

1. Identify user-controlled input.
2. Observe normal application behaviour.
3. Test with simple command payloads.
4. Determine whether the vulnerability is Blind or Verbose.
5. Analyse the application's responses.
6. Confirm command execution.
7. Document the findings and recommend mitigations.

Following a consistent methodology improves both the reliability and repeatability of security assessments.

---

## Skills Practiced

- Command Injection Assessment
- Blind Command Injection
- Verbose Command Injection
- Input Analysis
- HTTP Request Analysis
- Web Application Security

---

## Key Takeaways

- Practical Command Injection testing begins by understanding how an application processes user input.
- Application behaviour determines whether Blind or Verbose testing techniques should be used.
- Simple payloads are often sufficient to identify vulnerable functionality.
- A structured testing methodology produces more accurate and repeatable assessments.
- Successful testing should always be followed by appropriate remediation recommendations.