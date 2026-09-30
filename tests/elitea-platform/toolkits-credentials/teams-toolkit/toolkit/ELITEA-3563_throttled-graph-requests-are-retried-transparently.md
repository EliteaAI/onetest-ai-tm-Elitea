---
id: ELITEA-3563
title: "Throttled Graph Requests Are Retried Transparently"
priority: high
type: functional
module: teams-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3563: Throttled Graph Requests Are Retried Transparently

**Module:** Teams Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that a 429/503 throttling response from Microsoft Graph is retried automatically (honoring `Retry-After`) without the calling tool failing.

## Preconditions

- Teams toolkit enabled with an authorized credential
- Ability to trigger or simulate a 429/503 throttling response from Microsoft Graph (e.g. rapid repeated calls)

## Test Data

- N/A (scenario-based)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger a scenario likely to be throttled (e.g. rapid repeated Teams tool calls) or otherwise induce a 429/503 response | Graph responds with 429 or 503 and a `Retry-After` header |
| 2 | Observe the tool call's outcome | The tool call still completes successfully after the automatic retry, rather than surfacing the throttling error to the end user |

## Expected Final State

The throttled call ultimately succeeds with a normal result; no throttling error reaches the caller.

## Pass/Fail Criteria

**Pass:**
- The call completes successfully despite the underlying throttling response

**Fail:**
- The throttling error (429/503) is surfaced directly to the caller instead of being retried
