# 03 - Your First SIEM: Navigating Splunk

## Overview

A Security Information and Event Management (SIEM) platform centralises security data so analysts can search, correlate, and investigate events from different sources.

The room introduces Splunk and uses it to investigate the BOTSv1 dataset.

---

## Why a SIEM?

A SOC may receive logs from many different systems:

    Firewalls
    Windows Systems
    Web Servers
    Network Sensors
    Applications

Searching each system independently is not scalable.

A SIEM provides a central platform:

    Multiple Data Sources
           ↓
         SIEM
           ↓
    Search / Correlation
           ↓
    Investigation

---

## Splunk

Splunk provides a search interface where analysts can use SPL (Search Processing Language) to investigate events.

The lab uses the BOTSv1 dataset.

The dataset is stored in:

    index=botsv1

---

## Important Splunk Fields

### Index

The index stores events and allows efficient searching.

Example:

    index=botsv1

---

### Sourcetype

The sourcetype classifies the format of ingested data and controls how Splunk parses the events.

Examples include:

    WinEventLog:Security
    suricata
    access_combined

---

## Basic Search

A basic search against the BOTSv1 dataset:

    index=botsv1

---

## Count Events by Sourcetype

Use:

    index=botsv1
    | stats count by sourcetype

This helps identify the different data sources available in the dataset.

---

## Searching by Sourcetype

A search can be restricted to a specific sourcetype.

Example:

    index=botsv1 sourcetype=<sourcetype>

This allows an analyst to focus on a particular log source.

---

## SIEM Investigation Workflow

A basic workflow is:

    Identify Data Source
          ↓
    Search Events
          ↓
    Filter
          ↓
    Aggregate
          ↓
    Identify Pattern
          ↓
    Investigate

---

## Methodology

The important lesson is not simply learning Splunk syntax.

The analyst must first understand:

    What data exists?
    ↓
    Where is it stored?
    ↓
    Which sourcetype contains the evidence?
    ↓
    What query exposes the relevant pattern?

---

## Key Takeaways

- A SIEM centralises security data.
- Splunk uses SPL for searching and analysis.
- The BOTSv1 dataset is stored in `index=botsv1`.
- Sourcetype identifies the format and source of events.
- `stats` can aggregate events.
- Searching is only the beginning; the analyst must interpret the results.