# What is SQL Injection?

## Overview

SQL Injection (SQLi) is a web application vulnerability that occurs when user-supplied input is improperly incorporated into SQL queries. If input is not handled securely, an attacker may influence the execution of database commands, potentially exposing or modifying sensitive information.

This lesson introduces the fundamental concept of SQL Injection and provides an overview of the primary SQLi categories commonly encountered during web application security assessments.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Define SQL Injection and explain how it occurs
- Understand why insecure query construction creates security risks
- Differentiate between common SQL Injection categories
- Recognise the importance of secure database communication
- Understand the general process used to identify vulnerable database queries

---

## Main Content

### Understanding SQL Injection

Applications frequently accept user input and use it to build SQL queries that interact with a database.

When this input is incorporated into a query without proper protection, the database may interpret user-controlled data as part of the SQL command rather than as plain data.

---

### Why SQL Injection Is Dangerous

Improperly constructed queries can allow attackers to influence database behaviour beyond the application's intended functionality.

Possible consequences include:

- Access to confidential information
- Modification of stored data
- Authentication bypass
- Disclosure of database structure
- Compromise of application functionality

---

### Categories of SQL Injection

SQL Injection techniques are generally grouped into several categories depending on how information is returned by the application.

Common categories include:

- In-Band SQL Injection
- Blind SQL Injection
- Out-of-Band SQL Injection

Each category relies on different application behaviour but shares the same underlying weakness: insecure handling of SQL queries.

---

### Understanding the Methodology

Identifying SQL Injection vulnerabilities typically involves analysing how an application communicates with its database and observing how it responds to different forms of input.

Understanding database structure, query behaviour, and application responses is essential when assessing SQL Injection risks.

---

## Skills Practiced

- SQL Injection Fundamentals
- Database Query Analysis
- Web Application Security
- Vulnerability Classification
- Secure Database Concepts

---

## Key Takeaways

- SQL Injection occurs when user input becomes part of an SQL query without proper protection.
- The vulnerability exists because applications fail to separate executable SQL code from user-supplied data.
- SQL Injection techniques are commonly grouped into In-Band, Blind, and Out-of-Band categories.
- Understanding how applications construct SQL queries is essential for recognising SQL Injection vulnerabilities and applying secure development practices.