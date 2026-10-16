---
id: ELITEA-3854
title: "[EliteaAI/elitea_issues#5808] Status Update Persists on Backend"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3854: [EliteaAI/elitea_issues#5808] Status Update Persists on Backend

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that a test run status update persists on the qTest backend and remains unchanged after session reload.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project
- qTest Toolkit is enabled
- Access to qTest API for verification (GET endpoints)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `update_test_run_status(projectId=<valid>, testRunId=<valid>, status="Passed")` to update status. | Toolkit action succeeds; response confirms. |
| 2 | Wait 2 seconds for backend processing. | Backend has time to persist update. |
| 3 | Query qTest API: `GET /api/v3/projects/{projectId}/test-runs/{testRunId}` to retrieve test run details. | Status field in response shows "Passed". |
| 4 | Reload Elitea page (F5) to clear session. | Page reloads; session cleared. |
| 5 | Query qTest API again to retrieve test run details. | Status field still shows "Passed" (persisted). |
| 6 | Open qTest UI directly and navigate to test run. | Status visible in qTest UI as "Passed". |

## Expected Final State

- Status persisted on qTest backend
- Status remains unchanged after page reload
- Status visible in qTest UI

## Pass/Fail Criteria

**Pass:** Status persists on backend; unchanged after reload; visible in qTest UI.  
**Fail:** Status lost or reverted; backend query shows wrong value; UI shows different status.
