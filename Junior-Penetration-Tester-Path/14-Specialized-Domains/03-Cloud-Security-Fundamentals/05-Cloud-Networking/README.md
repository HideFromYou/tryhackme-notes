# 05 - Cloud Networking

## Overview

Cloud networking answers two important penetration-testing questions:

- What is actually reachable?
- What can we access after gaining a foothold?

The underlying networking concepts are similar across cloud providers even when the terminology differs.

---

## Building Blocks

### Virtual Network

A virtual network is the private network a customer creates inside the cloud provider's infrastructure.

It has its own IP address range and is isolated from other customers' virtual networks unless they are intentionally connected.

Provider terminology:

| Provider | Virtual Network |
|---|---|
| AWS | VPC |
| Azure | Virtual Network (VNet) |
| Google Cloud | VPC |

---

### Subnets

A subnet is a section of the virtual network.

They are commonly divided into:

- Public subnets
- Private subnets

A public subnet has a route to the Internet.

A private subnet does not have a direct Internet route.

Conceptually:

    Internet
       ↓
    Public Subnet
       ↓
    Private Subnet

Resources in a private subnet can communicate internally, but Internet hosts cannot directly reach them.

---

## Firewall Primitives

Two important firewall controls are:

- Security Groups
- Network ACLs (NACLs)

### Security Groups

Security Groups operate at the instance level.

They are stateful, meaning that if an outbound request is allowed, the corresponding response is automatically allowed back.

They use an implicit-deny model.

    Matching Allow Rule
           ↓
        Allowed

    No Matching Rule
           ↓
         Dropped

Security Groups can only explicitly allow traffic.

---

### Network ACLs

Network ACLs operate at the subnet level.

They are stateless, so traffic in both directions must be explicitly allowed.

Unlike Security Groups, NACLs support both:

    Allow
    Deny

NACLs therefore provide a broader subnet-level safety layer.

---

## Security Group vs NACL

| Feature | Security Group | Network ACL |
|---|---|---|
| Scope | Instance | Subnet |
| State | Stateful | Stateless |
| Rules | Allow | Allow / Deny |
| Main purpose | Instance-level filtering | Subnet-level filtering |

Security Groups are the main firewall control commonly encountered during cloud engagements, while NACLs act as a broader safety net.

---

# Attacker Focus 1 - Exposed Ports

One of the most common cloud misconfigurations is a Security Group rule allowing:

    0.0.0.0/0

This represents the entire Internet.

The first question when approaching a cloud target should therefore be:

    What is exposed?
    To whom?

---

## Common Examples

### SSH

    Port 22
    0.0.0.0/0

A bastion host may only need to accept connections from a specific jump server.

---

### Database Services

Common database ports include:

    3306   MySQL
    5432   PostgreSQL
    27017  MongoDB

A database exposed to:

    0.0.0.0/0

may be reachable from the entire Internet.

---

### Administrative Panels

Common examples include:

    8080
    9000

An administrative interface that should only be accessible through a VPN may accidentally become Internet-accessible.

---

### RDP

    3389

Old RDP rules may remain after migrations and unnecessarily expose systems.

---

## Enumeration

Cloud networking does not fundamentally change traditional reconnaissance.

The room specifically mentions:

    Port Scans
    HTTP Probes

The cloud mainly changes how easily configuration mistakes can be introduced.

---

# Attacker Focus 2 - Lateral Movement

Cloud networks can provide opportunities for lateral movement after an initial compromise.

A compromised instance may have access to many internal systems because the internal network can be relatively flat.

A compromised front-end server may be able to reach:

    Internal Databases
    Internal Caches
    Other Application Servers
    Internal-Only Admin Panels
    Service Metadata Endpoints

The key post-foothold question is:

    What else in this virtual network can I reach?

The answer may be more than expected.

---

## Lateral Movement

The attack concept is:

    Compromised Instance
            ↓
    Internal Network
            ↓
    Reachable Services
            ↓
    Other Systems

A cloud compromise therefore does not necessarily end with the first compromised machine.

---

# Provider Callouts

| Concept | AWS | Azure | Google Cloud |
|---|---|---|---|
| Virtual network | VPC | Virtual Network (VNet) | VPC |
| Subnet | Subnet | Subnet | Subnet |
| Internet access | Internet Gateway | Public IP / NAT Gateway | Default route + external IP / Cloud NAT |
| Instance firewall | Security Group | Network Security Group (NSG) | Firewall Rule |
| Subnet firewall | Network ACL (NACL) | NSG at subnet scope | Firewall Rule at network tag scope |

---

# Pentester Checklist

When assessing cloud networking:

    1. Identify the virtual network.

    2. Identify public and private subnets.

    3. Identify Internet-facing services.

    4. Check Security Group rules.

    5. Look for 0.0.0.0/0 exposure.

    6. Identify exposed SSH, database, RDP,
       and administrative services.

    7. After gaining a foothold, enumerate
       reachable internal services.

    8. Check for lateral-movement opportunities.

---

# Key Takeaways

- A virtual network provides private network isolation.
- Subnets divide the virtual network.
- Public subnets have Internet connectivity.
- Private subnets do not have direct Internet access.
- Security Groups are stateful instance-level firewalls.
- NACLs are stateless subnet-level controls.
- `0.0.0.0/0` represents the entire Internet.
- Exposed databases and administrative services are important findings.
- Traditional port scanning and HTTP probing still apply.
- A compromised cloud instance can provide access to internal resources.
- Always ask what else is reachable after gaining a foothold.

---

# Knowledge Check

## Question 1

Which CIDR notation indicates that a port is open to the entire Internet?

    0.0.0.0/0

## Question 2

What two-word term describes moving from one compromised instance to another reachable service inside the same virtual network?

    Lateral movement