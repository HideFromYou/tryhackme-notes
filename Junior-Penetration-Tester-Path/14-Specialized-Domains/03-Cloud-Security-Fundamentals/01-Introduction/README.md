# 01 - Introduction


## Overview


The cloud is essentially rented infrastructure.


When a company "runs in the cloud", it means that it pays a cloud provider such as **AWS, Azure, Google Cloud, or another provider** for compute, storage, and networking resources delivered through an API.


Instead of purchasing physical servers and maintaining them in a server room, a customer can provision resources such as a virtual machine within minutes.


From a penetration tester's perspective, this is important because modern engagements frequently cross cloud boundaries.


A company's environment may include:


- A public-facing web application running on a cloud virtual machine
- Files stored in an object storage bucket
- Identities managed through a cloud directory
- Internal cloud networking
- Cloud-based compute resources


If a penetration tester does not understand the primitives attackers abuse in these environments, important findings can be missed or security recommendations may not apply correctly.


---


## Cloud-Agnostic Approach


This room presents cloud security concepts in a **cloud-agnostic** way.


Instead of focusing on the implementation of one specific provider, the room uses generic concepts that apply across different cloud environments.


The room focuses on:


```text
Service Deployment Models
        ↓
Identity
        ↓
Storage
        ↓
Networking
        ↓
Compute

The concepts are then applied during a practical exercise against a simulated cloud environment.

Practical Exercise

The room concludes with a hands-on exercise against a simulated cloud environment.

The exercise demonstrates an attack chain involving:

Port Scanning
     ↓
Pivoting
     ↓
SSRF Chaining
     ↓
Exfiltration

The purpose is to connect the cloud concepts introduced throughout the room with a practical penetration-testing scenario.

Learning Objectives

By completing this room, you should be able to:

Shared Responsibility Model

Explain the Shared Responsibility Model and understand how responsibilities are distributed across:

IaaS
PaaS
SaaS
Identity and Access Management

Read an IAM policy, identify roles as an important attack primitive, and recognise over-permissive wildcard permissions.

Cloud Storage

Recognise publicly exposed cloud storage and understand how an attacker can enumerate it.

Cloud Networking

Describe common cloud networking primitives, exposed-service patterns, and lateral-movement scenarios.

Instance Metadata

Explain the Instance Metadata Service and understand the:

SSRF → Credentials

attack chain.

Practical Attack

Follow a guided, cloud-agnostic attack against a simulated cloud environment.

Learning Prerequisites

The room expects knowledge of:

Basic Linux commands
HTTP fundamentals
General penetration-testing concepts
An attacker mindset developed through earlier rooms in the Junior Penetration Tester path

Recommended foundations include:

Linux Fundamentals
HTTP Basics
Web Application Basics
Junior Penetration Tester Path
Key Concepts Introduced

The introduction establishes the main areas that will be explored throughout the room:

Area	Focus
Service Deployment Models	Understanding how cloud services are delivered
Identity	Understanding cloud identities, roles, and permissions
Storage	Identifying publicly exposed cloud storage
Networking	Understanding cloud networking and exposed services
Compute	Understanding cloud compute resources and metadata
SSRF	Understanding how server-side requests can interact with cloud infrastructure
Credentials	Understanding the SSRF-to-credentials attack chain
Pentesting Perspective

A cloud environment should not be treated as something completely separate from traditional penetration testing.

The same fundamental attacker mindset still applies:

Reconnaissance
      ↓
Enumeration
      ↓
Identify Weakness
      ↓
Exploit
      ↓
Pivot
      ↓
Access Additional Resources
      ↓
Exfiltration

The difference is that cloud environments introduce additional primitives such as:

Cloud APIs
IAM roles
Object storage
Metadata services
Cloud networking
Temporary credentials

Understanding these primitives allows a penetration tester to recognise vulnerabilities that may otherwise be missed.

Introduction Takeaways

The most important concepts from this section are:

Cloud environments provide compute, storage, and networking through APIs.
Modern penetration tests frequently involve cloud infrastructure.
Cloud security must be understood across different service models.
IAM roles and permissions are important attack primitives.
Public cloud storage can expose sensitive information.
Cloud networking introduces additional exposed-service and lateral-movement possibilities.
Instance Metadata Services can become highly sensitive when combined with SSRF.
Multiple weaknesses can be chained together during a cloud attack.