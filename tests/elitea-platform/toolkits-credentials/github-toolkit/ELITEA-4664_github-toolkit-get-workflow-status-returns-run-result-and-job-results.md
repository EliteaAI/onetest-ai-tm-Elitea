---
id: ELITEA-4664
title: "GitHub Toolkit — Get Workflow Status returns the run result and each job's result"
priority: medium
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4664: GitHub Toolkit — Get Workflow Status returns the run result and each job's result

**Module:** Github Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_workflow_status`, given a run ID from `get_workflow_runs`, returns the correct status, result, workflow and job results for runs that succeeded, failed or were cancelled.

**Coverage:**
- Failed run with job-level results
- Status, result and workflow name for every run type in the test data

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `get_workflow_runs` and `get_workflow_status` turned on
- The repo has the runs below. Run 43029359437 has job `build` (success) and job `test` (failure at step "Fail on purpose")

## Test Data
| Run ID | Expected status | Expected result | Expected workflow |
|---|---|---|---|
| 43029353955 | completed | success | Runs Test Data |
| 43029359437 | completed | failure | Runs Test Data |
| 43029369070 | completed | cancelled | Runs Test Data |
| 43029333302 | completed | success | CI |
| 43029333380 | completed | failure | Build |
| 20059899666 | completed | success | CI |
| 20059899697 | completed | failure | Build |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `get_workflow_status`. | The tool's input form opens. |
| 2 | Run the tool with `{"run_id": "43029359437"}`. | Status = completed, result = failure, workflow = Runs Test Data. |
| 3 | Check the job list in the step 2 response. | Job `build` has result success and job `test` has result failure. |
| 4 | Run the tool for each other run ID in the test data table. | Status, result and workflow match the table for every run. |

## Expected Final State
`get_workflow_status` reports the same status and result as GitHub Actions for every run.

## Pass/Fail Criteria

**Pass:**
- Every run matches the table, and run 43029359437 shows the correct per-job results

**Fail:**
- Any status, result, workflow or job result does not match GitHub, or the tool returns an error for a valid run ID
