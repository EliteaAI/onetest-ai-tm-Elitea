---
id: ELITEA-3937
title: "[EliteaAI/elitea_issues#5999] Runtime vs Connection Test Consistency"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:jira, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-3937: Runtime vs Connection Test Consistency

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that connection test result matches actual tool execution behavior (critical for user trust).

## Preconditions

- Jira Cloud and/or Server instance available
- Valid credentials configured
- Toolkit connection tests previously passing

## Test Data

| Scenario | Config | Expected Behavior |
|----------|--------|-------------------|
| Auto Cloud | Hosting=Auto, URL=*.atlassian.net, Version=Auto | Test: pass v2→v3, Runtime: use v3 |
| Auto Server | Hosting=Auto, URL=on-premise, Version=Auto | Test: pass v2, Runtime: use v2 |
| Explicit v3 | Version=3, Cloud URL | Test: pass v3, Runtime: use v3 |
| Explicit v2 | Version=2, Server URL | Test: pass v2, Runtime: use v2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For each configuration scenario above: configure toolkit. | Configuration saved. |
| 2 | Click "Test Connection" button and record result. | Connection test succeeds/fails as expected. |
| 3 | Save configuration. | Configuration persisted. |
| 4 | In Chat/Agent, call a read Jira tool. | Tool execution result matches connection test (same API version used). |
| 5 | Call a write Jira tool (comment or update). | Write operation succeeds/fails consistently with test. |
| 6 | Compare logs: connection test API version vs runtime API version. | Logs show SAME API version used in both test and runtime. |

## Expected Final State

- Connection test and runtime always agree on API version used
- If test passes, runtime should work (same API version)
- If test fails, runtime should fail the same way
- No surprises: manual config changes not needed after successful test

## Pass/Fail Criteria

**Pass:** Test and runtime use same API version, results consistent (both pass or both fail).  
**Fail:** Test passes but runtime fails, different API versions used, inconsistent behavior.

## Notes

- This is the critical consistency check
- Validates that test connection is a reliable predictor of runtime behavior
- Key for user trust in the feature
