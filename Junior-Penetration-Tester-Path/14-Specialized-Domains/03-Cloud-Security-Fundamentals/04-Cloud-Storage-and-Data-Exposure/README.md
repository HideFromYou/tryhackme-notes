# 04 - Cloud Storage and Data Exposure

## Overview

Cloud storage misconfigurations are a common source of data exposure. The main goal is to identify publicly accessible buckets and sensitive objects.

## Object Storage

Cloud providers use object storage to store files as objects inside storage containers.

Common terminology:

| Provider | Storage |
|---|---|
| AWS | S3 Bucket |
| Azure | Blob Container |
| Google Cloud | Cloud Storage Bucket |

## Access Controls

The main access-control mechanisms discussed in this room are:

- Bucket policies
- ACLs
- Signed / pre-signed URLs

A dangerous public-access configuration may contain:

    "Principal": "*"

Long-lived signed URLs can also expose resources if the URL becomes available to unauthorised users.

## Common Causes of Public Storage

### Development Defaults

A development bucket may be made public temporarily and later forgotten.

### Public Access Protection Disabled

Disabling provider protections can make storage publicly accessible.

### Wildcard Principal

A wildcard principal can allow access from arbitrary identities.

    "Principal": "*"

### Leaked Signed URLs

Signed URLs that remain valid for an excessive amount of time can eventually become exposed through logs, documentation, tickets, or other locations.

## Attacker Workflow

### 1. Identify Candidate Bucket Names

Common naming patterns include:

    <company>-backups
    <company>-dev
    <company>-prod
    <company>-assets

### 2. Probe Provider Endpoints

Check candidate bucket names using the provider's public endpoint format.

### 3. List Publicly Accessible Storage

If listing is allowed without authentication, enumerate the available objects.

### 4. Download Interesting Objects

Prioritise files that may contain sensitive information.

Useful tools mentioned in the room:

    s3scanner
    cloud_enum
    curl

## High-Value Objects

Prioritise:

1. Backups
2. Source code and build artefacts
3. Configuration files
4. Logs
5. Customer data

Examples of interesting configuration files:

    .env
    credentials.json

## Provider Mapping

| Concept | AWS | Azure | Google Cloud |
|---|---|---|---|
| Storage service | Amazon S3 | Azure Blob Storage | Google Cloud Storage |
| Storage unit | Bucket | Container | Bucket |
| Access mechanisms | Bucket Policy / IAM / ACL | SAS / RBAC / Public Access | IAM / ACL / Signed URL |

## Pentester Checklist

    Identify cloud provider
    ↓
    Identify storage services
    ↓
    Enumerate public buckets
    ↓
    Enumerate objects
    ↓
    Identify sensitive files
    ↓
    Check for exposed credentials
    ↓
    Follow the discovered attack path

## Key Takeaways

- Public cloud storage can expose sensitive information.
- Development environments are common sources of accidental exposure.
- Wildcard principals can create public access.
- Long-lived signed URLs can become an exposure point.
- Backups can contain large amounts of sensitive information.
- Storage enumeration should be part of cloud reconnaissance.