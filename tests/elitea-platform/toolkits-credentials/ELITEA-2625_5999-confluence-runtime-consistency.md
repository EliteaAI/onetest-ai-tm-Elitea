---
id: ELITEA-2625
title: "[EliteaAI/elitea_issues#5999] Confluence: Runtime vs Connection Test Consistency"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5999, r-2.0.6, feat:toolkits, int:confluence, eng:backend]
requirements: [EliteaAI/elitea_issues#5999]
---

# ELITEA-2625: Confluence — Runtime vs Connection Test Consistency

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that Confluence connection test result matches actual content operation behavior.

## Preconditions

- Confluence Cloud and/or Server instance available
- Valid credentials configured
- Toolkit connection tests previously passing

## Test Data

| Scenario | Config | Expected Behavior |
|----------|--------|-------------------|
| Auto Cloud | Hosting=Auto, URL=*.atlassian.net, Version=Auto | Test: pass with v2, Runtime: use v2 |
| Auto Server | Hosting=Auto, URL=on-premise, Version=Auto | Test: pass with v2, Runtime: use v2 |
| Explicit v2 | Version=2 (explicit) | Test: pass v2, Runtime: use v2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | For each configuration scenario: configure toolkit. | Configuration saved. |
| 2 | Click "Test Connection" button and record result. | Connection test succeeds/fails as expected. |
| 3 | Save configuration. | Configuration persisted. |
| 4 | In Chat/Agent, call a read Confluence tool. | Tool execution result matches connection test. |
| 5 | Call a write Confluence tool (create page/update). | Write operation succeeds/fails consistently with test. |
| 6 | Compare logs: connection test API version vs runtime. | Logs show SAME API version used. |

## Expected Final State

- Connection test and runtime always agree on API version
- If test passes, runtime works (same API version)
- If test fails, runtime fails the same way
- No surprises or manual config changes needed

## Pass/Fail Criteria

**Pass:** Test and runtime use same API version, results consistent.  
**Fail:** Test passes but runtime fails, different API versions, inconsistent behavior.

## Notes

- Critical consistency check
- Validates test connection is reliable predictor of runtime
- Key for user trust in the feature
