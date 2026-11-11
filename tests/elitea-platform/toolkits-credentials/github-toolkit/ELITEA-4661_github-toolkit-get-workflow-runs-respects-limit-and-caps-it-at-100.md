---
id: ELITEA-4661
title: "GitHub Toolkit — Get Workflow Runs respects the limit and caps it at 100"
priority: low
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407"]
---
# ELITEA-4661: GitHub Toolkit — Get Workflow Runs respects the limit and caps it at 100

**Module:** Github Toolkit · **Priority:** Low · **Type:** Functional

**Objective:** Verify that `get_workflow_runs` returns no more runs than `limit`, keeps the newest ones, and caps a too-large limit at 100 without an error.

**Coverage:**
- `limit` = 1 returns only the newest run
- `limit` above the maximum is capped at 100 with no error

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `get_workflow_runs` turned on
- Workflow `runs-test-data.yml` has the 3 runs listed in ELITEA-4659 (newest is 43029369070)

## Test Data
| Variant | Input | Expected |
|---|---|---|
| V1 limit 1 | `{"workflow_id": "runs-test-data.yml", "limit": 1}` | Exactly one run: 43029369070 |
| V2 limit 500 | `{"limit": 500}` | No error. At most 100 runs. If the repo has 100 runs or fewer, all of them |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `get_workflow_runs`. | The tool's input form opens. |
| 2 | Run the tool with V1. | Exactly one run is returned, and it is 43029369070 (the newest). |
| 3 | Run the tool with V2. | The tool finishes without an error or a GitHub validation message, and returns no more than 100 runs. |
| 4 | Compare the count from step 3 with the total on the repo's GitHub Actions page. | The count equals the total, or 100 if the repo has more than 100 runs. |

## Expected Final State
The tool honours small limits and silently caps large ones at 100.

## Pass/Fail Criteria

**Pass:**
- V1 returns only the newest run
- V2 returns 100 runs at most, with no error

**Fail:**
- V1 returns more than one run, or not the newest
- V2 returns an error or more than 100 runs
