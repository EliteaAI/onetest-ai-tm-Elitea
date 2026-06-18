---
id: ELITEA-1410
title: "ADO02 - List Open Pull Requests"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1410: ADO02 - List Open Pull Requests

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_open_pull_requests' tool retrieves open PRs

## Preconditions

ADO Repos toolkit is configured with valid credentials.
ADO_REPOSITORY_ID is set.
Test PR #10 with title 'PR FOR AI TEST' exists in the repository in open state.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with the target repository ID | Toolkit initialized successfully |
| 2 | Call `list_open_pull_requests` tool passing the repository_id | Tool executes and returns a list (may be empty but not an error) |
| 3 | Verify the response is a valid list/array (even if empty) | Result is a parseable array structure |
| 4 | Verify at least 1 open PR is returned | open_pr_count >= 1 |
| 5 | Verify PR #10 with title 'PR FOR AI TEST' is present in the list | pull_request_id = 10 and title = 'PR FOR AI TEST' found in results |

## Expected Final State

pull_request_id = 10 and title = 'PR FOR AI TEST' found in results

## Pass/Fail Criteria

test_passed = true
tool_executed = true
open_pr_count >= 1
title_check = true (PR title = 'PR FOR AI TEST')
id_check = true (pull_request_id = 10)
