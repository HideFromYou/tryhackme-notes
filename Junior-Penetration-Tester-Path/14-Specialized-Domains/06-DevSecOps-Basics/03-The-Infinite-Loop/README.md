# 03 - The Infinite Loop

## Overview

DevOps can be visualised as an infinite loop representing the continuous nature of development and operations.

The lesson introduces several important DevOps processes and technologies.

---

## CI/CD

CI/CD stands for:

    Continuous Integration
    Continuous Deployment

CI/CD supports frequent merging of small code changes and automated testing.

Instead of waiting until the end:

    Code Change
        ↓
    Merge
        ↓
    Automated Tests
        ↓
    Deployment

This allows bugs to be detected earlier.

### Benefits

    Early Bug Detection
    Automated Testing
    Smaller Changes
    Easier Rollbacks
    More Reliable Releases

---

## Infrastructure as Code

Infrastructure as Code (IaC) manages and provisions infrastructure using code and automation.

Instead of manually creating infrastructure:

    Code
      ↓
    Automated Provisioning
      ↓
    Consistent Infrastructure

Examples mentioned in the room include:

    Terraform
    Vagrant

IaC allows infrastructure definitions to be reused and consistently deployed.

---

## Configuration Management

Configuration management maintains the desired state of infrastructure and applies changes efficiently.

Benefits include:

    Consistency
    Maintainability
    Visibility
    Reduced Manual Work

IaC can also be used for configuration management.

---

## Orchestration

Orchestration automates workflows and coordinates different processes.

It can help systems respond automatically when conditions change.

For example:

    Health Check
        ↓
    Problem Detected
        ↓
    Automated Response

---

## Monitoring

Monitoring focuses on collecting data about the performance and stability of services and infrastructure.

Monitoring provides:

    Visibility
    Performance Data
    Stability Information
    Faster Recovery
    Root-Cause Analysis
    Automated Responses

---

## Microservices

Microservices architecture breaks an application into multiple small services.

Benefits include:

    Flexibility
    Scalability
    Reduced Complexity
    Technology Choice per Service

---

## Key Takeaways

- CI/CD automates testing and frequent code integration.
- IaC provisions infrastructure through reusable code.
- Configuration management maintains infrastructure state.
- Orchestration automates workflows.
- Monitoring collects performance and stability data.
- Microservices divide applications into smaller services.