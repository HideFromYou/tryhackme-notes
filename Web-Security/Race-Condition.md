# Race Condition Vulnerability Notes

## Overview

A race condition is a business logic vulnerability where concurrent requests interact with shared application state before it is properly updated.

This can result in inconsistent behavior, transaction abuse, authorization bypass, or unexpected application state.

---

## Core Concept

Example transaction logic:

1. Check available balance
2. Validate transaction
3. Process request
4. Update account state

Sequential requests:

Request 1:
- balance check passes
- transaction completes
- balance updates

Request 2:
- sees updated balance
- may be denied

Concurrent requests:

Multiple requests arrive nearly simultaneously:

- Request A sees original balance
- Request B sees original balance
- Request C sees original balance

before the balance is updated.

Result:

Multiple transactions may be incorrectly approved.

---

## Practical Learning

Hands-on concepts practiced:

- observing normal application transaction behavior
- capturing authenticated POST requests
- replaying requests in Burp Repeater
- grouped request testing
- parallel request execution
- state inconsistency observation
- balance manipulation through concurrent transaction logic

---

## Burp Workflow Used

1. Capture authenticated transfer request in Burp Proxy HTTP History
2. Send request to Repeater
3. Create request tab group
4. Duplicate request multiple times
5. Send grouped requests in parallel
6. Observe application responses and account state changes

---

## Key Lessons

- Race conditions are business logic vulnerabilities
- Timing matters
- Parallel requests behave differently from sequential requests
- Session state impacts exploitation
- Shared resources must be handled atomically
- Backend state can become inconsistent under concurrency

---

## Practical Behaviors Observed

Examples observed during testing:

- successful parallel transaction approvals
- negative balance states
- partial transaction success
- inconsistent account balances
- server instability under concurrent load
- internal server errors during race testing

---

## Tools Used

- Burp Suite Proxy
- Burp Repeater
- TryHackMe labs
