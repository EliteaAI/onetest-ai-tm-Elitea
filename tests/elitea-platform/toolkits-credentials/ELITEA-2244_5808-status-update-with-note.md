---
id: ELITEA-2244
title: "[EliteaAI/elitea_issues#5808] Status Update with Optional Note Parameter"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-2244: [EliteaAI/elitea_issues#5808] Status Update with Optional Note Parameter

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit accepts and stores an optional note parameter when updating test run status.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- qTest Toolkit is enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `update_test_run_status(projectId=<valid>, testRunId=<valid>, status="Failed", note="Test failed due to database connection timeout during login step")`. | Toolkit action executes without error. |
| 2 | Verify response includes: testRunId, status="Failed", note="..." | Response confirms status and note accepted. |
| 3 | Verify via qTest API (GET test run details) that note is stored with status. | Note persisted on qTest backend. |
| 4 | In qTest UI, open test run and verify note appears in execution log or status history. | Note visible in qTest UI. |

## Expected Final State

- Status updated to "Failed"
- Optional note parameter accepted and stored
- Note persists on qTest backend
- Note visible in qTest UI execution log

## Pass/Fail Criteria

**Pass:** Status updated; note accepted and stored; visible in qTest UI.  
**Fail:** Note rejected or lost; not persisted on backend; not visible in UI.
