---
id: ELITEA-3550
title: "No Stored Token Surfaces a Clean Re-Authorization Prompt Instead of Failing Inside a Tool Call"
priority: critical
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3550: No Stored Token Surfaces a Clean Re-Authorization Prompt Instead of Failing Inside a Tool Call

**Module:** Teams Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that loading the Teams toolkit with OAuth configured but no token available raises an authorization-required prompt proactively, before any tool executes.

## Preconditions

- A Teams toolkit/credential exists where OAuth discovery is set but no access token has been obtained yet (or the stored token has been cleared)

## Test Data

- N/A (state-based scenario)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure an Agent or Pipeline to use the token-less Teams toolkit/credential | Toolkit is attached without error at configuration time |
| 2 | Attempt to use any Teams tool (e.g. `list_teams`) from that Agent or Pipeline | Execution is intercepted before the Graph call; a re-authorization/login prompt is shown |
| 3 | Inspect the surfaced message/error | It clearly states OAuth authorization is required, rather than a raw exception or a failure occurring deep inside tool execution |

## Expected Final State

The run stops cleanly at the authorization boundary; no partial or malformed tool result is returned.

## Pass/Fail Criteria

**Pass:**
- User is shown a re-authorization/login prompt before the tool call reaches Graph

**Fail:**
- The call fails with a raw/generic error, or fails deep inside tool execution instead of at the authorization boundary
