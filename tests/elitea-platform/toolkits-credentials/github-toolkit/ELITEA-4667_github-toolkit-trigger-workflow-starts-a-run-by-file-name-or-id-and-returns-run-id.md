---
id: ELITEA-4667
title: "GitHub Toolkit — Trigger Workflow starts a run by file name or ID and the run appears in Get Workflow Runs"
priority: medium
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407", "EliteaAI/elitea_issues#7518"]
---
# ELITEA-4667: GitHub Toolkit — Trigger Workflow starts a run by file name or ID and the run appears in Get Workflow Runs

**Module:** Github Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `trigger_workflow` starts a new run when the workflow is given by file name or numeric ID, that the new run can be found with `get_workflow_runs`, and that the response gives the new run's ID.

**Coverage:**
- Trigger by file name
- Trigger by numeric workflow ID
- New run is listed by `get_workflow_runs`
- Response contains the new run ID

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `trigger_workflow` and `get_workflow_runs` turned on. The credential can run Actions in the repo
- Workflow `test-workflow.yml` (ID `189651695`) can be triggered by hand on `main`
- Known issue: the response has no run ID (step 3), tracked in #7518. Until it is fixed, step 3 fails

## Test Data
| Variant | Input |
|---|---|
| V1 file name | `{"workflow_id": "test-workflow.yml", "ref": "main"}` |
| V2 numeric ID | `{"workflow_id": "189651695", "ref": "main"}` |
| Check | `{"workflow_id": "test-workflow.yml", "limit": 1}` in `get_workflow_runs` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run `get_workflow_runs` with the Check input and note the newest run ID. | The current newest run ID is noted (or the list is empty). |
| 2 | Run `trigger_workflow` with V1. | The tool reports that the workflow was triggered on `main`. |
| 3 | Check the step 2 response for a run ID. | The response includes the ID of the new run. |
| 4 | Wait about 10 seconds, then run `get_workflow_runs` with the Check input. | A new run, newer than the one from step 1, is returned with `event` = `workflow_dispatch` and `head_branch` = `main`. If step 3 gave an ID, it matches. |
| 5 | Run `trigger_workflow` with V2, then repeat step 4. | The trigger succeeds and another new run appears. |

## Expected Final State
Two new runs of `test-workflow.yml` exist on `main`, and both can be found with `get_workflow_runs`.

## Teardown
- Cancel the new runs on GitHub if they are still running

## Pass/Fail Criteria

**Pass:**
- Both variants start a run that `get_workflow_runs` lists
- The trigger response contains the new run ID

**Fail:**
- Either variant fails, or reports success but no new run appears
- The response has no run ID
