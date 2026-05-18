# TryHackMe - AVenger

## Overview
Completed the AVenger TryHackMe challenge room, focusing on practical web exploitation, SQL injection discovery, authentication bypass, and post-exploitation troubleshooting.

This challenge simulated a realistic offensive security workflow involving vulnerability discovery, exploitation, and flag retrieval.

---

## Skills Practiced

- Web application enumeration
- SQL Injection discovery
- Authentication bypass
- Manual payload crafting
- Linux command-line interaction
- Post-exploitation troubleshooting
- Offensive security methodology

---

## Methodology

### Enumeration
Initial reconnaissance focused on identifying the application attack surface and vulnerable user-controlled inputs.

Actions performed:

- web application inspection
- parameter analysis
- authentication testing
- vulnerability discovery

This phase identified SQL Injection as the primary attack vector.

---

### SQL Injection Discovery
The login functionality accepted unsanitized user input directly into backend SQL queries.

Indicators included:

- abnormal authentication behavior
- injectable input fields
- controllable backend logic

This confirmed the presence of SQL Injection.

---

### Exploitation
The vulnerability was exploited by manipulating SQL authentication logic.

Payload used:

```text
' OR 1=1;--
```

This payload was injected into both:

- username field
- password field

Example vulnerable query:

```sql
SELECT * FROM users
WHERE username='$user'
AND password='$pass'
```

Injected effect:

```sql
WHERE username='' OR 1=1;--
AND password='' OR 1=1;--
```

Because:

```sql
1=1
```

always evaluates as TRUE, authentication was successfully bypassed, granting unauthorized access.

---

### Post-Exploitation
After successful authentication bypass, restricted functionality became accessible and a flag file was identified.

Initial attempt:

```bash
cat flag.txt
```

This did not reveal the expected output.

After troubleshooting, an alternative approach was used:

```bash
less flag.txt
```

This successfully displayed the final flag.

---

## Security Lessons Learned

### SQL Injection Prevention
Best defensive practices:

- Prepared statements
- Parameterized queries
- Input validation
- Escaping dangerous characters
- Least privilege database permissions

---

### Authentication Security
Authentication should never rely on dynamically concatenated SQL queries.

Unsafe:

```sql
SELECT * FROM users
WHERE username='$user'
AND password='$pass'
```

Safe:

```sql
SELECT * FROM users
WHERE username=? AND password=?
```

---

## Tools Used

- Browser
- Manual SQL payloads
- Linux shell utilities
- TryHackMe challenge environment

---

## Key Takeaways

This room reinforced practical understanding of:

- identifying SQL Injection vulnerabilities
- exploiting insecure authentication mechanisms
- abusing backend SQL logic
- adapting post-exploitation techniques when expected tooling fails
- thinking through a realistic offensive security attack chain
