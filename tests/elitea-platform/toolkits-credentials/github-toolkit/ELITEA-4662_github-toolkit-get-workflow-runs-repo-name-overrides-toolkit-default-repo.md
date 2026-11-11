---
id: ELITEA-4662
title: "GitHub Toolkit — Get Workflow Runs reads another repo when repo_name is given"
priority: low
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4662: GitHub Toolkit — Get Workflow Runs reads another repo when repo_name is given

**Module:** Github Toolkit · **Priority:** Low · **Type:** Functional

**Objective:** Verify that `repo_name` in `get_workflow_runs` overrides the toolkit's default repository.

**Coverage:**
- `repo_name` override of the toolkit's configured repository

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit whose default repository is **not** `SamvelSimonyan/testRepo` (any other repo the same credential can read), with `get_workflow_runs` turned on
- The credential can read `SamvelSimonyan/testRepo`, which has the runs listed in ELITEA-4660

## Test Data
| Field | Value |
|-------|-------|
| Input A (no override) | `{}` |
| Input B (override) | `{"repo_name": "SamvelSimonyan/testRepo"}` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the toolkit, go to Test Settings and select `get_workflow_runs`. | The tool's input form opens. |
| 2 | Run the tool with Input A. | Runs from the toolkit's default repo are returned (their `url` values contain that repo's name), or an empty list if it has no runs. |
| 3 | Run the tool with Input B. | Runs from `SamvelSimonyan/testRepo` are returned. Every `url` contains `SamvelSimonyan/testRepo/actions/runs/`, and run IDs from ELITEA-4660 appear. |
| 4 | Open the toolkit configuration again. | The default repository is unchanged. |

## Expected Final State
`repo_name` applies only to that call. The toolkit keeps its configured default repository.

## Pass/Fail Criteria

**Pass:**
- Input B returns testRepo's runs while the toolkit points at another repo

**Fail:**
- Input B returns the default repo's runs, or an error
- The toolkit's default repository changes after the call
