TryHackMe - Neighbour
Objective

Exploit an IDOR (Insecure Direct Object Reference) vulnerability to access another user's profile and retrieve the flag.

What I Learned
Reviewing page source code for hidden information
Identifying exposed credentials
Understanding IDOR vulnerabilities
Manipulating URL parameters
Bypassing authorization checks
Vulnerability: IDOR

IDOR (Insecure Direct Object Reference) occurs when an application exposes a direct reference to an object (user, file, record, profile, etc.) without properly verifying whether the current user is authorized to access it.

Example:

/profile?user=guest

If changing:

/profile?user=admin

grants access to another user's data, the application is vulnerable to IDOR.

Enumeration

Access the web application:

http://MACHINE_IP

The login page contains a hint suggesting viewing the source code.

View Source:

Ctrl + U

Inspecting the HTML reveals guest credentials.

Initial Access

Login using:

Username: guest
Password: guest

After authentication, the URL contains:

?user=guest
Exploitation

Since the room focuses on IDOR, test whether the application properly validates access controls.

Modify:

?user=guest

to:

?user=admin

The application loads the administrator profile and exposes the flag.

Attack Flow
View Source
      ↓
Find Guest Credentials
      ↓
Login as guest
      ↓
Observe URL Parameter
      ↓
Change guest → admin
      ↓
Access Admin Page
      ↓
Retrieve Flag
Key Takeaways
Always Inspect Source Code

Hidden comments, credentials, endpoints, and hints may be exposed in HTML.

Never Trust Client-Side Identifiers

Applications should never rely solely on:

?user=guest

for authorization decisions.

Authorization Must Be Server-Side

The server should verify:

Does the authenticated user own this resource?

before returning data.

Mitigations
Implement Access Control Checks

Verify ownership on every request.

Use Indirect References

Instead of:

/user?id=1

use random identifiers:

/user/7d2f9a8c
Principle of Least Privilege

Users should only access resources explicitly assigned to them.

Log Unauthorized Access Attempts

Monitor parameter tampering and suspicious requests.

MITRE ATT&CK
Technique	ID
Exploitation of Public-Facing Application	T1190
Valid Accounts (Abuse of Authorization Logic)	T1078
Commands / Actions Used
Ctrl + U
Login as guest
?user=guest
?user=admin
Summary

Neighbour is a beginner-friendly room demonstrating how an IDOR vulnerability can allow an attacker to access another user's data simply by modifying a URL parameter. The room reinforces the importance of proper server-side authorization and resource ownership validation.
