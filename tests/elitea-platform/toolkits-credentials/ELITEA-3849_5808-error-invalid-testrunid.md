---
id: ELITEA-3849
title: "[EliteaAI/elitea_issues#5808] Error Handling — Invalid testRunId"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3849: [EliteaAI/elitea_issues#5808] Error Handling — Invalid testRunId

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit returns a clear error message when an invalid testRunId is provided.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `update_test_run_status(projectId=<valid>, testRunId=999999, status="Passed")` with non-existent testRunId. | Toolkit action returns error. |
| 2 | Verify error response includes message indicating test run not found. | Error message is clear (e.g., "Test run ID 999999 not found"). |
| 3 | Verify no status update is applied to any test run. | System remains unchanged; no side effects. |
| 4 | Verify error message is actionable (suggests valid testRunId or how to find it). | Error message provides guidance. |

## Expected Final State

- Error returned for invalid testRunId
- No status update applied
- Clear, actionable error message provided

## Pass/Fail Criteria

**Pass:** Error returned; clear message; no status update; message is actionable.  
**Fail:** No error returned; vague error message; unexpected status update applied.
