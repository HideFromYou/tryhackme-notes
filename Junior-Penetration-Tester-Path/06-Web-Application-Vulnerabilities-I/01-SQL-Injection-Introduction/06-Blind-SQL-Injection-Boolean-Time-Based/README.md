# Blind SQL Injection: Boolean-Based & Time-Based

## Overview

Boolean-Based and Time-Based SQL Injection are advanced forms of Blind SQL Injection used when applications do not expose database errors or query results. Instead of relying on visible output, these techniques infer information by observing differences in application behaviour or response time.

This lesson explains the concepts behind both approaches and highlights how indirect application responses can reveal information about database queries.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the principles of Boolean-Based SQL Injection
- Explain how Time-Based SQL Injection differs from other SQLi techniques
- Recognise how application responses can be used to infer database behaviour
- Compare different Blind SQL Injection techniques
- Understand the limitations of behaviour-based testing

---

## Main Content

### Boolean-Based SQL Injection

Boolean-Based SQL Injection relies on applications producing different responses depending on whether a database condition evaluates to true or false.

Rather than displaying query results, the application reveals subtle behavioural differences that allow testers to determine how the database processes specific conditions.

---

### Time-Based SQL Injection

Time-Based SQL Injection is used when an application returns identical responses regardless of database conditions.

Instead of analysing page content, testers observe response times to determine whether specific database operations were executed.

Because timing differences become the primary source of information, consistency and repeated testing are often required to distinguish genuine results from normal network latency.

---

### Comparing Both Techniques

Although both methods belong to the Blind SQL Injection category, they rely on different indicators.

Boolean-Based techniques focus on:

- Changes in page content
- Different application responses
- Success or failure conditions

Time-Based techniques focus on:

- Response delays
- Timing consistency
- Observable execution differences

---

### Practical Considerations

Blind SQL Injection techniques generally require more requests and careful observation than In-Band SQL Injection.

Environmental factors such as caching, application behaviour, and network conditions may also influence the reliability of observed results.

---

## Skills Practiced

- Blind SQL Injection Concepts
- Boolean Logic
- Response Analysis
- Timing Analysis
- Web Application Security

---

## Key Takeaways

- Boolean-Based SQL Injection relies on true or false application responses.
- Time-Based SQL Injection infers database behaviour through response timing.
- Both techniques operate without directly exposing database output.
- Careful observation and methodical testing improve the reliability of Blind SQL Injection assessments.
- Understanding these techniques helps security professionals evaluate applications that provide minimal feedback during database interactions.