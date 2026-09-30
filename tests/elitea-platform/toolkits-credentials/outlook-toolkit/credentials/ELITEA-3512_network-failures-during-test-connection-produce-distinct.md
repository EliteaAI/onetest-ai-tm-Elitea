---
id: ELITEA-3512
title: "Network Failures During Test Connection Produce Distinct, Handled Messages"
priority: high
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3512: Network Failures During Test Connection Produce Distinct, Handled Messages

**Module:** Outlook Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify timeout and connection-error cases during `_call_graph_api` return specific handled error text rather than an unhandled exception.

## Preconditions

- A valid, authorized Outlook credential (token present)
- Ability to simulate network conditions to `graph.microsoft.com`

## Test Data

- Existing authorized Outlook credential

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Simulate a slow/unreachable Graph endpoint (block network to `graph.microsoft.com`, or use conditions causing the Graph call to time out) | Network condition is active |
| 2 | Trigger Test Connection | Request is attempted against Graph |
| 3 | Observe the result after ~10 seconds | A distinct "timeout"-style message is shown, not a raw stack trace |
| 4 | Repeat with a DNS/connection failure instead of a timeout | A distinct "connection error"-style message is shown, not a raw stack trace |

## Expected Final State

Both network failure modes surface as clear, handled error text.

## Pass/Fail Criteria

**Pass:**
- Timeout after ~10s produces a distinct, handled "timeout" message
- Connection failure produces a distinct, handled "connection error" message
- Neither case shows a raw stack trace to the user

**Fail:**
- Either failure mode shows an unhandled exception/stack trace
- Timeout and connection error are indistinguishable to the user
