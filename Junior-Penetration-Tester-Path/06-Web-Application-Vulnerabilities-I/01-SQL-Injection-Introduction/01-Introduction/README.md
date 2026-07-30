# Introduction

## Overview

This lesson introduces SQL Injection (SQLi), one of the most well-known vulnerabilities affecting database-driven web applications. It explains how insecure handling of user input can alter SQL queries and why SQL Injection remains a significant security risk despite being a long-established attack technique.

Understanding the fundamentals of SQL Injection provides the foundation for learning how different SQLi techniques work and how they can be prevented.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Define SQL Injection and its impact on web applications
- Understand how user input interacts with SQL queries
- Recognise the potential consequences of SQL Injection vulnerabilities
- Explain why SQL Injection continues to affect modern applications
- Understand the importance of secure database interaction

---

## Main Content

### What Is SQL Injection?

SQL Injection is a web application vulnerability that occurs when user-controlled input is incorporated into SQL queries without proper validation or parameterisation.

If an application treats user input as executable SQL instead of data, an attacker may influence how the database processes requests.

---

### Why It Matters

Successful SQL Injection attacks can affect the confidentiality, integrity, and availability of data stored within a database.

Potential impacts include:

- Unauthorised access to sensitive information
- Authentication bypass
- Modification or deletion of stored data
- Exposure of database structure
- Compromise of critical application functionality

---

### Why SQL Injection Still Exists

Although secure development practices are widely available, SQL Injection continues to appear in modern applications due to insecure coding practices, legacy software, and improper handling of database queries.

For security professionals, understanding this vulnerability is essential because it remains one of the most frequently tested weaknesses during web application assessments.

---

## Skills Practiced

- SQL Injection Fundamentals
- Database Security Concepts
- Web Application Security
- Vulnerability Awareness
- Secure Development Principles

---

## Key Takeaways

- SQL Injection occurs when user input is interpreted as part of an SQL query.
- Poor input handling can expose sensitive databases to serious attacks.
- Understanding SQL Injection is fundamental for both penetration testing and secure software development.
- Preventing SQL Injection requires secure coding practices and proper database interaction techniques.