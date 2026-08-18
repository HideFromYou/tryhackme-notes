# Grep (THM)


## Overview


This room focused on web enumeration, OSINT, API key discovery, file upload restrictions, source-code analysis, and credential discovery.


My overall attack path was:


    Port Enumeration
        ↓
    grep.thm
        ↓
    Web Enumeration
        ↓
    API Key Discovery
        ↓
    GitHub / OSINT
        ↓
    API Key Reuse
        ↓
    Registration
        ↓
    File Upload
        ↓
    Source Code Analysis
        ↓
    Upload Filter Bypass
        ↓
    SQL Backup
        ↓
    Admin Email
        ↓
    leakchecker.grep.thm
        ↓
    Password Leak
        ↓
    Admin Password


---


# 1. Enumeration


I started with a port scan:


```bash
nmap -sV <TARGET_IP>

The interesting ports were:

80
443
51337

The scan also revealed the hostname:

grep.thm

I added it to /etc/hosts:

sudo nano /etc/hosts
<TARGET_IP> grep.thm

I then accessed the web application through:

http://grep.thm
2. Web Enumeration

I enumerated the website for hidden directories and files.

One interesting endpoint discovered was:

upload.php

The registration functionality was also interesting.

When I tried to register a new account, the application returned an error indicating that the API key was:

Expired / Invalid

This suggested that the registration functionality required a valid API key.

3. API Key Discovery

I intercepted the registration request with Burp Suite.

The request contained an API key parameter.

Since the website appeared to be a PHP application, I searched online for the application/source code.

The GitHub repository contained the relevant source code.

Looking through the commit history, I found an API key inside a previous version of:

register.php

The API key was:

ffe60ecaa8bba2f12b43d1a4b15b8f39
Answer
ffe60ecaa8bba2f12b43d1a4b15b8f39

This was an example of using OSINT and source-code history to recover a secret that was no longer valid in the current application.

4. Registration

I returned to Burp Suite and replaced the invalid API key with the recovered one.

I then forwarded the modified request.

The registration functionality worked and I obtained access to the application.

The first flag was:

THM{4ec9806d7e1350270dc402ba870ccebb}
5. File Upload

From the earlier directory enumeration, I had discovered:

upload.php

I tested whether I could upload a PHP reverse shell.

The initial upload attempts were blocked.

I tried changing:

Filename
Content-Type
File Content

but the application continued to reject the file.

This suggested that the server was inspecting the actual contents of the uploaded file rather than relying only on the extension or MIME type.

6. Analysing the Upload Filter

I went back to the source code on GitHub.

The upload functionality contained a check against the file's hexadecimal signature.

This explained why simply changing:

.php

or:

Content-Type

was not enough.

The application was checking the initial bytes of the uploaded file.

I modified the beginning of the file so that it matched an accepted file signature.

After bypassing the initial filter, I investigated where uploaded files were stored.

The uploaded files were accessible under:

/uploads
7. PHP Execution

Opening the uploaded file initially did not execute it as PHP.

The modification of the file header had also affected the PHP opening tag:

<?php

which made the file invalid PHP.

I therefore modified the payload so that the PHP code appeared after several comments while preserving the required file signature at the beginning.

This allowed the file to pass the upload validation while retaining valid PHP code.

8. Backup Files

While enumerating the available files, I discovered a backup directory.

Inside it was a SQL database backup.

I inspected the SQL file for useful application information.

One useful piece of information was the administrator's email address.

Question

What is the email of the "admin" user?

The email was:

admin@searchme2023cms.grep.thm
9. leakchecker.grep.thm

During the investigation I also discovered a directory/application named:

leakchecker

The service was associated with port:

51337

I added the subdomain to /etc/hosts:

<TARGET_IP> leakchecker.grep.thm

I could then access:

http://leakchecker.grep.thm:51337

The application allowed users to check whether an email address appeared in a password leak.

10. Admin Password

I used the administrator email discovered from the SQL backup:

admin@searchme2023cms.grep.thm

The leak-checking functionality returned a password associated with the account.

The password was:

admin_tryhackme!
Answer
admin_tryhackme!

I then attempted to use the recovered credentials to log in as the administrator.

The login functionality appeared to be incomplete / not fully implemented.

Answers
Question	Answer
API key	ffe60ecaa8bba2f12b43d1a4b15b8f39
First flag	THM{4ec9806d7e1350270dc402ba870ccebb}
Admin email	admin@searchme2023cms.grep.thm
Leak checker hostname	leakchecker.grep.thm
Admin password	admin_tryhackme!
Key Techniques
Enumeration
nmap -sV <TARGET_IP>

Identify:

Open Ports
Services
Hostnames
OSINT

The application name and technology were used to search for publicly available source code.

The GitHub repository was particularly useful because the API key was exposed in commit history.

Source Code Analysis

Source code helped explain:

API Authentication
File Upload Validation
Hexadecimal File Signature Checks

When application behaviour does not make sense from the outside, source-code analysis can explain exactly what the application is checking.

File Upload Bypass

The application validated the hexadecimal signature of uploaded files.

Therefore:

Extension Change
    ✗


MIME-Type Change
    ✗


Modify File Signature
    ✓

The challenge demonstrated why file-upload testing should include analysis of the actual server-side validation logic.

Attack Chain
Nmap
  ↓
grep.thm
  ↓
Web Enumeration
  ↓
Registration Endpoint
  ↓
Invalid API Key
  ↓
GitHub / OSINT
  ↓
Old register.php Commit
  ↓
API Key
  ↓
Burp Suite
  ↓
Registration
  ↓
First Flag
  ↓
upload.php
  ↓
Upload Filter
  ↓
Source Code Analysis
  ↓
Hex Signature Bypass
  ↓
/uploads
  ↓
Backup SQL
  ↓
Admin Email
  ↓
leakchecker.grep.thm
  ↓
Password Leak
  ↓
Admin Password
Key Takeaways
Enumerate all exposed ports, not just HTTP/HTTPS.
Hostnames discovered during enumeration can reveal virtual hosts.
Burp Suite is useful for understanding application requests and parameters.
Invalid API keys can be a clue that credentials or secrets exist elsewhere.
Search public repositories when authorised testing identifies an application with exposed source code.
Git history can contain secrets that were removed from the current version.
File-upload validation should be tested beyond filename and MIME type checks.
Source-code analysis can reveal exactly how upload filters work.
Backup files can expose sensitive application data.
Subdomains and non-standard ports should also be investigated.
Leaked credentials can provide another path even when the application's login functionality is incomplete.