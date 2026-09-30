---
id: ELITEA-3505
title: "Missing OAuth Discovery Endpoint Is Explicitly Rejected"
priority: critical
type: functional
module: outlook-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3505: Missing OAuth Discovery Endpoint Is Explicitly Rejected

**Module:** Outlook Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify testing a connection without an OAuth discovery endpoint returns the specific error "OAuth discovery endpoint is required for Outlook", not a generic failure.

## Preconditions

- N/A

## Test Data

- Client ID: `test-client-id`
- Client Secret: `test-client-secret`
- OAuth Discovery Endpoint: left blank

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create/edit an Outlook credential with Client ID and Client Secret filled but OAuth Discovery Endpoint left blank (if the UI allows saving in this state) | Credential form accepts the state (or blocks save per client-side validation) |
| 2 | Trigger Test Connection / `check_connection` | Request is processed |
| 3 | Inspect the returned error | Error text is exactly "OAuth discovery endpoint is required for Outlook" |

## Expected Final State

No token is stored; the credential remains unauthorized with a specific, actionable error message displayed.

## Pass/Fail Criteria

**Pass:**
- Error message is exactly "OAuth discovery endpoint is required for Outlook"

**Fail:**
- A generic error (e.g. "connection failed") is shown instead
- The request succeeds despite the missing endpoint
