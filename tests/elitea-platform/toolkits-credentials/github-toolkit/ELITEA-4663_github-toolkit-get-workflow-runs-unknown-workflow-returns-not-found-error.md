---
id: ELITEA-4663
title: "GitHub Toolkit — Get Workflow Runs returns a clear error for an unknown workflow"
priority: medium
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4663: GitHub Toolkit — Get Workflow Runs returns a clear error for an unknown workflow

**Module:** Github Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_workflow_runs` with a workflow that does not exist returns a readable "not found" message instead of an empty list or a raw exception.

**Coverage:**
- Unknown workflow file name

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `get_workflow_runs` turned on
- The repo has no workflow named `does-not-exist.yml`

## Test Data
| Field | Value |
|-------|-------|
| Input | `{"workflow_id": "does-not-exist.yml"}` |
| Expected message | Workflow `does-not-exist.yml` not found in repository SamvelSimonyan/testRepo |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `get_workflow_runs`. | The tool's input form opens. |
| 2 | Run the tool with the input above. | The tool returns an error that names the workflow and the repository, as in "Expected message". |
| 3 | Check the response text. | It has no Python traceback, no raw exception class name and no list of runs. |

## Expected Final State
The user is told that the workflow does not exist in the repository.

## Pass/Fail Criteria

**Pass:**
- A readable "Workflow … not found in repository SamvelSimonyan/testRepo" error is returned

**Fail:**
- An empty list, runs from other workflows, or a raw traceback is returned
