---
id: ELITEA-3840
title: "[EliteaAI/elitea_issues#5808] Update Test Run Status — All 9 Values"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5808, r-2.0.5, feat:toolkits, int:qtest, eng:api]
requirements: [EliteaAI/elitea_issues#5808]
---

# ELITEA-3840: [EliteaAI/elitea_issues#5808] Update Test Run Status — All 9 Values

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the qTest toolkit can successfully update a test run status to all 9 supported status values: Passed, Failed, Skipped, Blocked, Broken, No Result, Pending, Unknown, Incomplete.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- Valid qTest credentials configured and tested
- Test run exists in qTest project with known testRunId
- qTest Toolkit is enabled in Agent or Chat

## Test Data

| Status Value | Expected Behavior |
|--------------|-------------------|
| Passed | Marks test as successful |
| Failed | Marks test as failed |
| Skipped | Marks test as skipped |
| Blocked | Marks test as blocked |
| Broken | Marks test as broken/defective |
| No Result | Marks test as not run |
| Pending | Marks test as pending execution |
| Unknown | Marks test status as unknown |
| Incomplete | Marks test as incomplete |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Elitea Agent/Chat with qTest Toolkit enabled. | qTest toolkit available for use. |
| 2 | For each status value in [Passed, Failed, Skipped, Blocked, Broken, No Result, Pending, Unknown, Incomplete]: Call `update_test_run_status(projectId=<valid>, testRunId=<valid>, status=<value>)` | Toolkit action executes without error. |
| 3 | Verify response for first status (e.g., Passed): Response includes testRunId, status="Passed", timestamp. | Response confirms status update successfully. |
| 4 | Verify response structure is consistent for all 9 statuses. | All status updates follow same response format. |
| 5 | For each status update, verify via qTest API (GET /api/v3/projects/{projectId}/test-runs/{testRunId}) that status persisted on backend. | Each status value is correctly stored on qTest backend. |
| 6 | Confirm no error messages appear for any of the 9 status values. | All 9 statuses are accepted and processed successfully. |

## Expected Final State

- All 9 test run status values successfully updated
- Each status update returns confirmation with correct status value
- Each status persists on qTest backend
- No errors or rejections for any valid status value

## Pass/Fail Criteria

**Pass:** All 9 status values successfully update test run; responses confirm status; backend persistence verified for all.  
**Fail:** Any status value fails; responses inconsistent; backend persistence fails; error messages appear.
