---
id: ELITEA-4668
title: "GitHub Toolkit — Trigger Workflow returns an error for an unknown workflow or branch"
priority: low
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407", "EliteaAI/elitea_issues#7518"]
---
# ELITEA-4668: GitHub Toolkit — Trigger Workflow returns an error for an unknown workflow or branch

**Module:** Github Toolkit · **Priority:** Low · **Type:** Functional

**Objective:** Verify that `trigger_workflow` reports an error, and does not claim success, when the workflow or the branch does not exist.

**Coverage:**
- Unknown workflow file name
- Unknown branch (`ref`)

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `trigger_workflow` and `get_workflow_runs` turned on
- The repo has no workflow `does-not-exist.yml` and no branch `branch-does-not-exist-xyz`
- Known issue: V2 currently reports success, tracked in #7518. Until it is fixed, V2 fails

## Test Data
| Variant | Input | Expected |
|---|---|---|
| V1 unknown workflow | `{"workflow_id": "does-not-exist.yml", "ref": "main"}` | "Workflow … not found" error |
| V2 unknown branch | `{"workflow_id": "test-workflow.yml", "ref": "branch-does-not-exist-xyz"}` | Error that says no ref was found |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `trigger_workflow`. | The tool's input form opens. |
| 2 | Run V1. | A "Workflow … not found" error is returned. |
| 3 | Run V2. | An error is returned that says the ref `branch-does-not-exist-xyz` was not found. The tool does not say the workflow was triggered. |
| 4 | Run `get_workflow_runs` with `{"workflow_id": "test-workflow.yml", "limit": 1}`. | No new run was created by steps 2 and 3. |

## Expected Final State
No runs are started, and the user is told why.

## Pass/Fail Criteria

**Pass:**
- Both variants return an error that names the problem, and no run is created

**Fail:**
- Either variant reports success, or a run is created
