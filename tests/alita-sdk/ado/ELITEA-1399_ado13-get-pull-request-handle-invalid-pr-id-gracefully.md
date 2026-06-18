---
id: ELITEA-1399
title: "ADO13 - get_pull_request: Handle invalid PR ID gracefully"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, negative-test, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1399: ADO13 - get_pull_request: Handle invalid PR ID gracefully

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_pull_request' tool handles invalid PR ID gracefully.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
PR ID 999999 does NOT exist in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_pull_request` tool with an invalid pull_request_id = '999999' (non-existent PR) | Tool executes but returns an error or empty response |
| 3 | Verify the response contains an error indicator (e.g., 'not found', 'does not exist', '404', or null/empty) | At least one error indicator is present in the response |
| 4 | Verify no valid PR object with a real pullRequestId is returned | Response does not contain a valid PR structure matching a real PR |
| 5 | Verify the tool did not throw an unhandled exception (no 'traceback' or 'stack trace') | Response does not contain 'traceback' or 'unhandled' |

## Expected Final State

Response does not contain 'traceback' or 'unhandled'

## Pass/Fail Criteria

test_passed = true
tool_executed = true (no crash)
graceful_handling = true
no_valid_pr_returned = true
no_unhandled_exception = true
