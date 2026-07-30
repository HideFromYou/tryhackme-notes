# Remediation and Prevention

## Overview

Understanding how SQL Injection occurs is only part of securing web applications. Equally important is knowing how to prevent these vulnerabilities through secure coding practices, proper database configuration, and layered security controls.

This lesson introduces the primary defensive techniques used to reduce the risk of SQL Injection and improve the overall security of database-driven applications.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand the importance of parameterised queries
- Explain the role of input validation
- Recognise the purpose of output escaping
- Understand the Principle of Least Privilege
- Identify how multiple security controls work together to reduce SQL Injection risk

---

## Main Content

### Parameterised Queries

Parameterised (prepared) statements separate SQL instructions from user-supplied data.

By ensuring that input is always treated as data rather than executable SQL, parameterised queries provide the most effective defence against SQL Injection.

---

### Input Validation

Applications should validate user input before processing it.

Validation ensures that submitted values conform to expected formats, reducing the likelihood of unexpected or malicious input reaching the database.

Input validation should complement secure query construction rather than replace it.

---

### Escaping User Input

Escaping special characters helps prevent them from being interpreted as SQL syntax.

Although escaping can reduce certain risks, it should not be considered a complete substitute for parameterised queries because implementation varies across database systems.

---

### Principle of Least Privilege

Applications should connect to databases using accounts with only the permissions required to perform their intended tasks.

Restricting database privileges limits the potential impact of a successful attack by reducing access to sensitive resources.

---

### Defence in Depth

Protecting applications against SQL Injection involves multiple layers of security working together.

Common defensive measures include:

- Parameterised queries
- Input validation
- Secure error handling
- Least privilege
- Security monitoring
- Web Application Firewalls (WAFs)

Combining these controls provides stronger protection than relying on any single mechanism.

---

## Skills Practiced

- Secure Coding Concepts
- SQL Injection Mitigation
- Input Validation
- Database Security
- Defence in Depth

---

## Key Takeaways

- Parameterised queries are the primary defence against SQL Injection.
- Input validation improves application security when combined with secure query construction.
- Database permissions should follow the Principle of Least Privilege.
- Multiple defensive controls provide stronger protection than any single security measure.
- Preventing SQL Injection requires secure development practices throughout the application lifecycle.