---
id: ELITEA-3555
title: "Expired Access Token Is Automatically Refreshed During Tool Execution"
priority: critical
type: functional
module: teams-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6785]
---
# ELITEA-3555: Expired Access Token Is Automatically Refreshed During Tool Execution

**Module:** Teams Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the stored access token expires mid-use, the SDK transparently refreshes it via the stored `refresh_token` and retries the original call, without requiring the user to re-authorize.

## Preconditions

- A Teams credential exists with `auto_refresh_token` enabled and a valid `refresh_token` stored

## Test Data

- N/A (state-based scenario)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Force or wait for the stored access token to expire, leaving the refresh token valid | Credential's access token is now expired, refresh token remains valid |
| 2 | Call any Teams tool (e.g. `list_teams`) from an Agent or Pipeline | A new access token is obtained via the refresh token and the original request is retried automatically |
| 3 | Confirm the call result | The call succeeds transparently and the user is not prompted to re-authorize |

## Expected Final State

The credential holds a newly refreshed access token; the tool call returns a normal successful result.

## Pass/Fail Criteria

**Pass:**
- The expired-token call completes successfully with no re-authorization prompt

**Fail:**
- The call fails, or the user is prompted to re-authorize despite having a valid refresh token
