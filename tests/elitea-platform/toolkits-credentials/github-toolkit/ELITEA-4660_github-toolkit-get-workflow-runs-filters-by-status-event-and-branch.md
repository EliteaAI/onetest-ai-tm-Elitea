---
id: ELITEA-4660
title: "GitHub Toolkit — Get Workflow Runs filters runs by status, event and branch"
priority: medium
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4660: GitHub Toolkit — Get Workflow Runs filters runs by status, event and branch

**Module:** Github Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_workflow_runs` without a `workflow_id` lists runs from all workflows in the repo, and that the `status`, `event` and `branch` filters return only matching runs.

**Coverage:**
- Filter by `status` (result value such as `failure`, `cancelled`)
- Filter by `event`, combined with `limit`
- Filter by `branch`
- Default limit of 10 when no limit is given

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `get_workflow_runs` turned on
- The repo has these runs:

| Run ID | Workflow | Event | Branch | Result |
|---|---|---|---|---|
| 43029353955 | Runs Test Data | workflow_dispatch | main | success |
| 43029359437 | Runs Test Data | workflow_dispatch | main | failure |
| 43029369070 | Runs Test Data | workflow_dispatch | main | cancelled |
| 43029333302 | CI | push | main | success |
| 43029333380 | Build | push | main | failure |
| 20059899666 / 20059899697 | CI / Build | pull_request | featurefile-branch | success / failure |

## Test Data
| Variant | Input | Expected |
|---|---|---|
| V1 status failure | `{"status": "failure"}` | Only runs with `conclusion` = `failure`. At most 10 runs (default limit) |
| V2 status cancelled | `{"status": "cancelled"}` | Exactly one run: 43029369070 |
| V3 event + limit | `{"event": "push", "limit": 2}` | Exactly 2 runs, both with `event` = `push` |
| V4 branch | `{"branch": "featurefile-branch"}` | Exactly 2 runs (20059899666, 20059899697), both with `head_branch` = `featurefile-branch` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `get_workflow_runs`. | The tool's input form opens. |
| 2 | Run the tool with V1. | Every returned run has `conclusion` = `failure`. No more than 10 runs are returned. Runs from more than one workflow can appear. |
| 3 | Run the tool with V2. | Only run 43029369070 is returned. |
| 4 | Run the tool with V3. | Exactly 2 runs are returned and both have `event` = `push`. |
| 5 | Run the tool with V4. | Exactly 2 runs are returned and both have `head_branch` = `featurefile-branch`. |

## Expected Final State
Each filter narrows the repo-wide run list to only the matching runs, and the default and explicit limits are respected.

## Pass/Fail Criteria

**Pass:**
- Every variant returns only runs that match its filter, with the expected count

**Fail:**
- Any variant returns a run that does not match the filter, returns an error, or ignores the limit
