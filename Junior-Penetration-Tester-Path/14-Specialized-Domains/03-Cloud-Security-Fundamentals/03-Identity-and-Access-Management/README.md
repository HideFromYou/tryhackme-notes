# 03 - Identity and Access Management (IAM)


## Overview


Identity is where most cloud compromises start.


A leaked access key or a role with excessive permissions can provide an attacker with significant access without requiring a traditional memory-corruption exploit.


From a penetration tester's perspective, the minimum mental model is:


- Read an IAM policy
- Understand what a role allows
- Identify what permissions credentials provide
- Determine what to investigate first after obtaining credentials


---


## IAM Policies


A cloud IAM policy is a JSON document that specifies:


```text
Who can do what
to which resources

Three fields carry most of the meaning:

Field	Meaning
Effect	Allow or Deny
Action	Operations covered by the policy
Resource	Resource the action applies to

Examples of actions:

storage:GetObject
iam:CreateUser
Well-Scoped Policy

A well-scoped policy limits both the action and the resource:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "storage:GetObject",
      "Resource": "bucket/reports/*"
    }
  ]
}

This grants a single action against a specific bucket prefix.

Over-Permissive Policy

Compare this with:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}

The wildcard values dramatically increase the blast radius.

Action:   *
Resource: *

This means that the identity holding the policy can perform any action against any resource.

What to Look For

When reading a policy, immediately check:

Action:   *
Resource: *

Wildcards in these fields can indicate an over-permissive policy.

Provider Differences

The policy examples above use the AWS IAM policy structure.

The room uses:

storage:

as a generic service prefix.

Real providers use their own naming conventions.

Concept	AWS	Azure	Google Cloud
Identity service	IAM	Microsoft Entra ID	Cloud IAM
Long-lived credential	Access Key ID + Secret	Client ID + Secret, or user login	Service account key, or user login
Role equivalent	IAM Role	Managed Identity	Service Account

The syntax differs between providers, but the process of analysing permissions remains transferable.

Roles and Role Assumption

A role is a named bundle of permissions that an identity can temporarily assume.

Instead of giving a long-lived user every permission it might ever need, organisations can:

Create Role
    ↓
Attach Policies
    ↓
Allow Identity / Workload to Assume Role
    ↓
Receive Temporary Credentials
Why Role Assumption Matters

There are two important reasons to care about role assumption during an engagement.

Privilege Escalation

A compromised user or workload may be allowed to assume a more privileged role.

Compromised Identity
        ↓
   Assume Role
        ↓
More Privileged Access

This can provide a privilege-escalation path.

Instance Metadata

The Instance Metadata Service can provide temporary credentials for the role attached to a virtual machine.

Instance Metadata Service
        ↓
Temporary Credentials
        ↓
Role Permissions
IAM Enumeration Mindset

Whenever we obtain cloud credentials, the first question should be:

"What can I do with these?"

Credentials may originate from:

Leaked .aws/credentials
        ↓
SSRF response
        ↓
Compromised service

Once credentials are obtained, determine:

Which identity do these credentials belong to?

Then investigate:

What policies are attached?
Are policies attached directly or through a group?
Which roles can this identity assume?
Are any policies over-permissive?
Are there wildcards?
Which resources are in scope?
Is access limited to a single resource
or does it cover the whole account?

The room focuses on this enumeration pattern rather than provider-specific commands.

The Key IAM Attack Pattern

The main IAM attack pattern to remember is:

Over-Permissive Policy
        +
Exposed Credentials
        ↓
Potential Cloud Compromise

Access keys can end up in many locations.

Public Code Repositories
Public Repository
        ↓
Committed Credentials
        ↓
Exposed Access Key
Container Images
Public Container Registry
        ↓
Container Image
        ↓
Embedded Credentials
Configuration Files
Configuration File
        ↓
Backup
        ↓
Public Storage
        ↓
Exposed Credentials
Screenshots

Credentials can also accidentally appear in screenshots posted to tickets.

Why Exposed Credentials Matter

The keys themselves are simply strings.

The security impact depends on the permissions of the identity behind them.

For example:

Developer Access Key
        ↓
Identity with Wildcard Action
        ↓
Company Storage
        ↓
Potential Data Exposure

Therefore, finding exposed credentials should be followed by permission enumeration.

Pentester IAM Checklist

When landing a set of cloud credentials:

1. Identify the associated identity.


2. Identify attached policies.


3. Check whether policies are attached
   directly or through a group.


4. Identify assumable roles.


5. Look for over-permissive policies.


6. Look for wildcard permissions.


7. Identify accessible resources.


8. Determine whether access is limited
   to a specific resource or the whole account.
Core Attack Chain

The IAM concepts connect together as:

Exposed Credentials
        ↓
Identify Identity
        ↓
Enumerate Permissions
        ↓
Find Over-Permissive Policy
        ↓
Identify Accessible Resources
        ↓
Check Role Assumption
        ↓
Potential Privilege Escalation
Key Takeaways
IAM controls access to cloud resources.
IAM policies define permissions.
Effect, Action, and Resource are the key fields to understand.
Wildcards can dramatically increase the blast radius of a policy.
Roles provide temporary bundles of permissions.
Role assumption can become a privilege-escalation path.
Instance Metadata Services can provide temporary credentials for attached roles.
Exposed credentials should always be investigated for their permissions.
The most important pattern is:
Exposed Credentials
        +
Over-Permissive IAM
        ↓
Potential Cloud Compromise
Knowledge Check
Question 1

In an IAM policy statement, which field states whether access is allowed or denied?

Answer: Effect
Question 2

A named, temporary bundle of permissions that an identity can assume is called what?

Answer: Role


Αυτό είναι το **ολόκληρο repository content για το 03**, έτοιμο να μπει αυτούσιο στο:


```text
03-Cloud-Security-Fundamentals/
└── 03-Identity-and-Access-Management/
    └── README.md

Και πλέον όλα τα technical examples, JSON, commands και attack flows είναι μέσα σε code blocks.

ολο μεσα σε code block να το πιανω ολο με ενα ψοπy paste click 
# 03 - Identity and Access Management (IAM)


## Overview


Identity is where most cloud compromises start.


A leaked access key or a role with excessive permissions can provide an attacker with significant access without requiring a traditional memory-corruption exploit.


From a penetration tester's perspective, the minimum mental model is:


- Read an IAM policy
- Understand what a role allows
- Identify what permissions credentials provide
- Determine what to investigate first after obtaining credentials


---


## IAM Policies


A cloud IAM policy is a JSON document that specifies:


```text
Who can do what
to which resources

Three fields carry most of the meaning:

Field	Meaning
Effect	Allow or Deny
Action	Operations covered by the policy
Resource	Resource the action applies to

Examples of actions:

storage:GetObject
iam:CreateUser
Well-Scoped Policy

A well-scoped policy limits both the action and the resource:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "storage:GetObject",
      "Resource": "bucket/reports/*"
    }
  ]
}

This grants a single action against a specific bucket prefix.

Over-Permissive Policy

Compare this with:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}

The wildcard values dramatically increase the blast radius.

Action:   *
Resource: *

This means that the identity holding the policy can perform any action against any resource.

What to Look For

When reading a policy, immediately check:

Action:   *
Resource: *

Wildcards in these fields can indicate an over-permissive policy.

Provider Differences

The policy examples above use the AWS IAM policy structure.

The room uses:

storage:

as a generic service prefix.

Real providers use their own naming conventions.

Concept	AWS	Azure	Google Cloud
Identity service	IAM	Microsoft Entra ID	Cloud IAM
Long-lived credential	Access Key ID + Secret	Client ID + Secret, or user login	Service account key, or user login
Role equivalent	IAM Role	Managed Identity	Service Account

The syntax differs between providers, but the process of analysing permissions remains transferable.

Roles and Role Assumption

A role is a named bundle of permissions that an identity can temporarily assume.

Instead of giving a long-lived user every permission it might ever need, organisations can:

Create Role
    ↓
Attach Policies
    ↓
Allow Identity / Workload to Assume Role
    ↓
Receive Temporary Credentials
Why Role Assumption Matters

There are two important reasons to care about role assumption during an engagement.

Privilege Escalation

A compromised user or workload may be allowed to assume a more privileged role.

Compromised Identity
        ↓
   Assume Role
        ↓
More Privileged Access

This can provide a privilege-escalation path.

Instance Metadata

The Instance Metadata Service can provide temporary credentials for the role attached to a virtual machine.

Instance Metadata Service
        ↓
Temporary Credentials
        ↓
Role Permissions
IAM Enumeration Mindset

Whenever we obtain cloud credentials, the first question should be:

"What can I do with these?"

Credentials may originate from:

Leaked .aws/credentials
        ↓
SSRF response
        ↓
Compromised service

Once credentials are obtained, determine:

Which identity do these credentials belong to?

Then investigate:

What policies are attached?
Are policies attached directly or through a group?
Which roles can this identity assume?
Are any policies over-permissive?
Are there wildcards?
Which resources are in scope?
Is access limited to a single resource
or does it cover the whole account?

The room focuses on this enumeration pattern rather than provider-specific commands.

The Key IAM Attack Pattern

The main IAM attack pattern to remember is:

Over-Permissive Policy
        +
Exposed Credentials
        ↓
Potential Cloud Compromise

Access keys can end up in many locations.

Public Code Repositories
Public Repository
        ↓
Committed Credentials
        ↓
Exposed Access Key
Container Images
Public Container Registry
        ↓
Container Image
        ↓
Embedded Credentials
Configuration Files
Configuration File
        ↓
Backup
        ↓
Public Storage
        ↓
Exposed Credentials
Screenshots

Credentials can also accidentally appear in screenshots posted to tickets.

Why Exposed Credentials Matter

The keys themselves are simply strings.

The security impact depends on the permissions of the identity behind them.

For example:

Developer Access Key
        ↓
Identity with Wildcard Action
        ↓
Company Storage
        ↓
Potential Data Exposure

Therefore, finding exposed credentials should be followed by permission enumeration.

Pentester IAM Checklist

When landing a set of cloud credentials:

1. Identify the associated identity.


2. Identify attached policies.


3. Check whether policies are attached
   directly or through a group.


4. Identify assumable roles.


5. Look for over-permissive policies.


6. Look for wildcard permissions.


7. Identify accessible resources.


8. Determine whether access is limited
   to a specific resource or the whole account.
Core Attack Chain

The IAM concepts connect together as:

Exposed Credentials
        ↓
Identify Identity
        ↓
Enumerate Permissions
        ↓
Find Over-Permissive Policy
        ↓
Identify Accessible Resources
        ↓
Check Role Assumption
        ↓
Potential Privilege Escalation
Key Takeaways
IAM controls access to cloud resources.
IAM policies define permissions.
Effect, Action, and Resource are the key fields to understand.
Wildcards can dramatically increase the blast radius of a policy.
Roles provide temporary bundles of permissions.
Role assumption can become a privilege-escalation path.
Instance Metadata Services can provide temporary credentials for attached roles.
Exposed credentials should always be investigated for their permissions.
The most important pattern is:
Exposed Credentials
        +
Over-Permissive IAM
        ↓
Potential Cloud Compromise
Knowledge Check
Question 1

In an IAM policy statement, which field states whether access is allowed or denied?

Answer: Effect
Question 2

A named, temporary bundle of permissions that an identity can assume is called what?

Answer: Role

