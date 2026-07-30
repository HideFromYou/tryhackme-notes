# SQL Essentials for Injection

## Overview

Before understanding SQL Injection techniques, it is important to become familiar with several SQL features that are commonly encountered during database interactions. These concepts explain how SQL queries are structured and why certain language features are frequently associated with SQL Injection attacks.

This lesson introduces key SQL operators, functions, and database metadata that provide the foundation for understanding more advanced SQL Injection scenarios.

---

## Learning Objectives

After completing this lesson, you should be able to:

- Understand SQL comments and their purpose
- Explain how the UNION operator combines query results
- Recognise the role of pattern matching with LIKE
- Understand how LIMIT controls query output
- Identify common SQL string functions
- Describe the purpose of the information_schema database

---

## Main Content

### SQL Comments

Comments allow developers to annotate SQL code or temporarily ignore portions of a query during execution.

Depending on the database engine, SQL supports both single-line and multi-line comments. Understanding comment syntax helps explain how SQL queries are interpreted by the database engine.

---

### UNION Operator

The `UNION` operator combines the results of multiple `SELECT` statements into a single result set.

To produce valid results, each query must return the same number of columns with compatible data types.

This feature is commonly used in legitimate database operations to merge information from multiple queries.

---

### Pattern Matching with LIKE

The `LIKE` operator enables pattern-based searches within text values.

Wildcards can be used to match characters or groups of characters, making `LIKE` useful for flexible search functionality inside applications.

---

### Limiting Query Results

The `LIMIT` clause restricts the number of rows returned by a query.

Applications frequently use this feature to improve performance, implement pagination, or retrieve specific records from large datasets.

---

### SQL String Functions

SQL provides built-in functions for manipulating and combining text.

Common string functions allow applications to:

- Concatenate values
- Format output
- Aggregate multiple values
- Improve data presentation

These functions are widely used during normal database operations.

---

### Database Metadata

Most relational database systems maintain internal metadata describing their own structure.

This metadata contains information such as:

- Databases
- Tables
- Columns
- Data types
- Relationships

Understanding database metadata helps explain how applications organise and manage stored information.

---

## Skills Practiced

- SQL Fundamentals
- Query Structure
- Database Concepts
- SQL Operators
- Pattern Matching
- Database Metadata

---

## Key Takeaways

- SQL Injection relies on understanding how SQL queries are constructed.
- SQL operators and functions play an important role in database interactions.
- Metadata databases describe the structure of relational databases.
- A solid understanding of SQL fundamentals makes it easier to recognise insecure query handling and understand how secure database applications should operate.