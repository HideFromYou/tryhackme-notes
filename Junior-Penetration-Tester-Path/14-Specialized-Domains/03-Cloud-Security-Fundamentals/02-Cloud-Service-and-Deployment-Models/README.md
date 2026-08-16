# 02 - Cloud Service and Deployment Models

## Introduction

Every cloud engagement starts with two questions:

- What is the customer actually renting?
- Where does the cloud provider's responsibility stop?

Understanding **service models** and **deployment models** gives us the vocabulary needed to answer these questions and identify where cloud misconfigurations are likely to exist. :contentReference[oaicite:0]{index=0}

---

# Service Models

The three main service models are:

- IaaS
- PaaS
- SaaS

## IaaS — Infrastructure as a Service

With **IaaS**, the provider gives the customer basic computing infrastructure such as:

- Virtual machine
- Virtual disk
- Virtual network

The customer installs and manages everything running on top of that infrastructure.

A useful analogy is renting an empty apartment: the basic structure exists, but everything else is your responsibility.

### Example

A cloud virtual machine running the customer's own web stack.

---

## PaaS — Platform as a Service

With **PaaS**, the provider manages more of the underlying environment, including:

- Operating system
- Runtime
- Often scaling

The customer uploads their code or data and the provider runs it.

A useful analogy is a semi-furnished apartment: the basic infrastructure is already prepared, allowing the customer to focus on their application.

---

## SaaS — Software as a Service

With **SaaS**, the provider manages the complete application environment:

- Infrastructure
- Platform
- Software

The customer generally interacts with the application through a web interface and configures the available settings.

A useful analogy is renting a hotel room: the environment is already prepared and maintained by the provider.

Cloud-hosted email and collaboration suites are examples of this model. :contentReference[oaicite:1]{index=1}

---

# Deployment Models

Deployment models describe **who else shares the underlying infrastructure**.

## Public Cloud

Infrastructure is operated by a cloud provider and shared between customers.

Customer workloads run alongside workloads belonging to other customers, separated through mechanisms such as the hypervisor and network controls.

---

## Private Cloud

Infrastructure is dedicated to a single organisation.

It may be:

- Run on-premises
- Hosted externally

---

## Hybrid Cloud

A hybrid cloud combines public cloud and on-premises infrastructure.

Some workloads run in the public cloud while others remain on-premises.

The environments can be connected through mechanisms such as:

- Private links
- VPNs

---

## Community Cloud

A community cloud provides shared infrastructure for organisations with common requirements.

Examples include environments designed for:

- Government organisations
- Regulated industries

:contentReference[oaicite:2]{index=2}

---

# Shared Responsibility Model

One of the most important concepts in cloud security is the **Shared Responsibility Model**.

Many cloud security incidents occur because customers misunderstand where their responsibility begins and ends.

The provider is always responsible for:

- Physical data centre
- Hardware
- Hypervisor

The customer is always responsible for:

- Data
- Identities
- Access policies

The area between these responsibilities changes depending on the service model.

This includes areas such as:

- Operating system
- Runtime
- Network configuration

:contentReference[oaicite:3]{index=3}

---

# Responsibility Matrix

| Layer | IaaS | PaaS | SaaS |
|---|---|---|---|
| Physical datacentre | Provider | Provider | Provider |
| Hardware and hypervisor | Provider | Provider | Provider |
| Network Configuration | Customer | Shared | Provider |
| Operating system | Customer | Provider | Provider |
| Runtime and middleware | Customer | Provider | Provider |
| Application code | Customer | Customer | Provider |
| Data | Customer | Customer | Customer |
| Identities and access | Customer | Customer | Customer |

:contentReference[oaicite:4]{index=4}

---

# Pentester Perspective

As penetration testers, we normally do not find vulnerabilities in the cloud provider's hypervisor during a standard engagement.

Instead, we look for vulnerabilities and misconfigurations in the areas where the **customer is responsible**.

Examples include:

```text
Virtual machine
    ↓
Default password

Storage bucket
    ↓
Publicly accessible

IAM policy
    ↓
Wildcard action

Provider Examples

Different providers use different names for equivalent concepts.

Model	AWS	Azure	Google Cloud
IaaS	EC2 instance	Azure Virtual Machine	Compute Engine VM
PaaS	RDS, Elastic Beanstalk	Azure SQL Database, App Service	Cloud SQL, App Engine
SaaS	Amazon WorkMail	Microsoft 365	Google Workspace

Key Takeaways
IaaS

The customer manages more of the environment, including the operating system and runtime.

PaaS

The provider manages the operating system and runtime while the customer focuses more on their application and data.

SaaS

The provider manages the complete application environment.

Deployment Models
Public
Private
Hybrid
Community
Shared Responsibility

The provider secures the underlying physical infrastructure, while the customer remains responsible for their data, identities, and access policies.

The exact responsibility for the middle layers depends on the service model.