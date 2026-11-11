---
id: ELITEA-4669
title: "GitHub Toolkit — Generic API call with get_workflow_runs returns the run list"
priority: low
type: functional
module: github-toolkit
status: draft
execution_type: manual
tags: [enhancement:2407, feat:toolkits, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#2407", "EliteaAI/elitea_issues#7519"]
---
# ELITEA-4669: GitHub Toolkit — Generic API call with get_workflow_runs returns the run list

**Module:** Github Toolkit · **Priority:** Low · **Type:** Functional

**Objective:** Verify the second fix option in #2407: `generic_github_api_call` with method `get_workflow_runs` returns the list of runs instead of the "raw_data attribute is missing" error.

**Coverage:**
- Generic call that returns a paginated list (not a single object)

## Preconditions
- Logged in to `{{base_url}}` as a project member who can edit toolkits
- A GitHub toolkit connected to repo `SamvelSimonyan/testRepo`, with `generic_github_api_call` turned on
- The basic generic call (`get_repo`) is covered by ELITEA-1497 and is not repeated here
- Known issue: the code currently returns "raw_data attribute is missing" for list results, tracked in #7519. Until it is fixed, this case fails

## Test Data
| Field | Value |
|-------|-------|
| Input | `{"method": "get_workflow_runs", "method_kwargs": {}}` |
| Compare with | `get_workflow_runs` with `{"limit": 10}` |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the GitHub toolkit, go to Test Settings and select `generic_github_api_call`. | The tool's input form opens. |
| 2 | Run the tool with the input above. | A list of workflow runs is returned. |
| 3 | Check the response text. | It does not contain "raw_data attribute is missing" or a traceback. |
| 4 | Run `get_workflow_runs` with `{"limit": 10}` and compare the run IDs. | The newest run IDs from both calls match. |

## Expected Final State
The generic call can be used to list workflow runs.

## Pass/Fail Criteria

**Pass:**
- The generic call returns runs that match `get_workflow_runs`

**Fail:**
- The response is the "raw_data attribute is missing" error, any other error, or empty when runs exist
