---
id: ELITEA-2246
title: "[EliteaAI/elitea_issues#5808] Error Handling — Invalid Status Value"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-2246: [EliteaAI/elitea_issues#5808] Error Handling — Invalid Status Value

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit returns a clear error message when an invalid status value is provided.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `update_test_run_status(projectId=<valid>, testRunId=<valid>, status="InvalidStatus")` with unsupported status value. | Toolkit action returns error. |
| 2 | Verify error response includes validation message. | Error message indicates invalid status. |
| 3 | Verify error message lists all 9 allowed status values. | Error message educates user on valid values. |
| 4 | Verify no status update is applied. | Test run status remains unchanged. |

## Expected Final State

- Error returned for invalid status value
- No status update applied
- Clear error message listing all 9 allowed values

## Pass/Fail Criteria

**Pass:** Error returned; all 9 valid values listed; no status update applied.  
**Fail:** No error returned; allowed values not listed; unexpected status update.
