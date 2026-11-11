---
id: ELITEA-4665
title: "GitHub Toolkit — Workflow status and logs tools reject an invalid run ID with a clear error"
priority: low
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407", "EliteaAI/elitea_issues#7520"]
---
# ELITEA-4665: GitHub Toolkit — Workflow status and logs tools reject an invalid run ID with a clear error

**Module:** Github Toolkit · **Priority:** Low · **Type:** Functional

**Objective:** Verify that `get_workflow_status` and `get_workflow_logs` return a clear error when the run ID is a workflow ID (not a run) or is not a number.

**Coverage:**
- Workflow ID passed as a run ID (a common mistake before `get_workflow_runs` existed)
- Non-numeric run ID

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `get_workflow_status` and `get_workflow_logs` turned on
- `189651695` is a workflow ID in the repo, not a run ID
- Known issue: V3 currently returns a raw Python error, tracked in #7520. Until it is fixed, V3 fails

## Test Data
| Variant | Tool | Input | Expected |
|---|---|---|---|
| V1 | `get_workflow_status` | `{"run_id": "189651695"}` | 404 Not Found error |
| V2 | `get_workflow_logs` | `{"run_id": "189651695"}` | 404 Not Found error |
| V3 | `get_workflow_status` | `{"run_id": "abc"}` | Validation error saying the run ID must be a number |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit and go to Test Settings. | Test Settings opens. |
| 2 | Run V1. | A "Not Found" (404) error is returned, not data for a different run. |
| 3 | Run V2. | A "Not Found" (404) error is returned, with no log content. |
| 4 | Run V3. | A readable validation error is returned that says the run ID must be numeric. |
| 5 | Check the responses from steps 2 to 4. | None has a Python traceback or raw exception text such as `invalid literal for int()`. |

## Expected Final State
Invalid run IDs are rejected with messages the user can act on.

## Pass/Fail Criteria

**Pass:**
- V1 and V2 return 404 Not Found
- V3 returns a clear validation message

**Fail:**
- Any variant returns data, a success message or a raw Python error
