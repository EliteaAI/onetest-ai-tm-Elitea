---
id: ELITEA-1400
title: "ADO12 - get_pull_request: Retrieve PR details by ID"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1400: ADO12 - get_pull_request: Retrieve PR details by ID

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_pull_request' tool retrieves pull request details by ID.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Pull request #10 exists in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_pull_request` tool with pull_request_id = '10' | Tool executes without error |
| 3 | Verify the response contains the PR title | PR title 'PR FOR AI TEST' is present in the response |
| 4 | Verify the response contains the status (e.g., 'active' or 'completed') | PR status field is present |
| 5 | Verify the response contains source and target branch information | Branch information is present in the PR details |
| 6 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
pr_details_present = true (id, title, status returned)
no_error = true
