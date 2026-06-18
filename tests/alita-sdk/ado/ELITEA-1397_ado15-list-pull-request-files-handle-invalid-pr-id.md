---
id: ELITEA-1397
title: "ADO15 - list_pull_request_files: Handle invalid PR ID"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, negative-test, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1397: ADO15 - list_pull_request_files: Handle invalid PR ID

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_pull_request_files' tool handles invalid PR ID gracefully.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
PR ID 999999 does NOT exist in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `list_pull_request_files` tool with invalid pull_request_id = '999999' | Tool executes but returns an error or empty response (does not crash) |
| 3 | Verify the response contains an error indicator or empty structure (e.g., 'not found', '404', '[]', or null) | At least one expected error indicator is present |
| 4 | Verify the tool did not throw an unhandled exception | Response does not contain 'traceback' or 'stack trace' |

## Expected Final State

Response does not contain 'traceback' or 'stack trace'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
graceful_handling = true
no_unhandled_exception = true
