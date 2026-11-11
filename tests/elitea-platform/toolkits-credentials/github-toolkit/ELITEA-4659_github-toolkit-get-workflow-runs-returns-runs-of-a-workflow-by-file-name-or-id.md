---
id: ELITEA-4659
title: "GitHub Toolkit — Get Workflow Runs returns the runs of one workflow by file name or numeric ID"
priority: high
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4659: GitHub Toolkit — Get Workflow Runs returns the runs of one workflow by file name or numeric ID

**Module:** Github Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that the new `get_workflow_runs` tool lists the runs of one workflow, newest first, with every documented field, whether the workflow is given by file name or by numeric ID.

**Coverage:**
- Lookup by workflow file name
- Lookup by numeric workflow ID gives the same result
- Sort order (newest first)
- Fields returned for each run

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with the `get_workflow_runs` tool turned on (SDK 0.12.15 or later)
- Workflow `runs-test-data.yml` (ID `414705771`) is in the repo. It runs only when triggered by hand, with input `outcome` = `success`, `failure` or `slow`
- The workflow has exactly 3 runs: 43029353955 (success), 43029359437 (failure), 43029369070 (cancelled). If it has more, compare against the GitHub Actions page instead of the IDs below

## Test Data
| Field | Value |
|-------|-------|
| Input A (file name) | `{"workflow_id": "runs-test-data.yml"}` |
| Input B (numeric ID) | `{"workflow_id": "414705771"}` |
| Expected order | 43029369070, 43029359437, 43029353955 |
| Required fields | `id`, `name`, `workflow_id`, `run_number`, `event`, `status`, `conclusion`, `head_branch`, `head_sha`, `created_at`, `updated_at`, `url` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit and go to Test Settings. Select the `get_workflow_runs` tool. | The tool's input form opens. |
| 2 | Run the tool with Input A. | The tool finishes without an error and returns 3 runs. |
| 3 | Check the order of the returned run IDs. | The order is 43029369070, 43029359437, 43029353955 (newest `created_at` first). |
| 4 | Check that each run has every field in "Required fields". | All 12 fields are present for every run. `name` is "Runs Test Data", `workflow_id` is 414705771 and `url` points to the run on github.com. |
| 5 | Run the tool with Input B. | The tool returns the same 3 runs, in the same order, as in step 2. |

## Expected Final State
`get_workflow_runs` returns the same complete, newest-first list of runs for the workflow, whether it is given by file name or by numeric ID.

## Pass/Fail Criteria

**Pass:**
- Both inputs return the same 3 runs, newest first
- Every run has all 12 required fields

**Fail:**
- Either input returns an error, an empty list or runs from other workflows
- The order is wrong, or any required field is missing
