---
id: ELITEA-4666
title: "GitHub Toolkit — Get Workflow Logs shows the failed step and returns only failed-job logs on request"
priority: medium
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4666: GitHub Toolkit — Get Workflow Logs shows the failed step and returns only failed-job logs on request

**Module:** Github Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `get_workflow_logs` shows run details with per-step results, and that `include_logs` with `failed_only` returns the log text of the failed job only.

**Coverage:**
- Step results without logs (failed step, skipped steps after it)
- Log text with `include_logs: true` and `failed_only: true`

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `get_workflow_logs` turned on
- Run 43029359437 failed: job `build` succeeded; job `test` failed at step "Fail on purpose", and the 2 steps after it were skipped
- Known issue: the note text in the response is misleading, tracked in #7521. It does not affect this case's result

## Test Data
| Variant | Input |
|---|---|
| V1 steps only | `{"run_id": "43029359437"}` |
| V2 failed logs | `{"run_id": "43029359437", "include_logs": true, "failed_only": true}` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `get_workflow_logs`. | The tool's input form opens. |
| 2 | Run V1. | Run details are returned (ID, workflow, result failure) with the jobs and their steps. |
| 3 | Find job `test` in the step 2 response. | Step "Fail on purpose" has result failure, and the 2 steps after it are marked skipped. |
| 4 | Run V2. | Log text is returned for job `test` only. Job `build` has no log text. |
| 5 | Search the step 4 log text for `exit code 1`. | `exit code 1` is present. |

## Expected Final State
The user can see which step failed and read the failed job's log without opening GitHub.

## Pass/Fail Criteria

**Pass:**
- V1 shows the failed step and the skipped steps
- V2 returns only the failed job's log, and it contains `exit code 1`

**Fail:**
- Step results do not match GitHub
- V2 includes logs for job `build`, returns no logs, or returns an error
