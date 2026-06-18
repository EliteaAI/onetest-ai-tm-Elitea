---
id: ELITEA-1404
title: "ADO08 - Create Pull Request Validation (non-destructive)"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, negative-test, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1404: ADO08 - Create Pull Request Validation (non-destructive)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'create_pr' tool returns an informative error when source and target branches are identical (non-destructive check)

## Preconditions

ADO Repos toolkit is configured with valid credentials.
This is a non-destructive test - uses identical source and target branch to trigger a validation error.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `create_pr` tool with source_branch = 'main' and target_branch = 'main' (identical branches) | Tool executes but returns an error (or handle gracefully) |
| 3 | Verify the response contains an informative error message about identical branches | Error message is present (e.g., 'source and target branches must be different' or similar) |
| 4 | Verify no actual PR was created (no pull_request_id returned) | Result does not contain a valid new pull_request_id |
| 5 | Verify the tool did not throw an unhandled exception | Result does not contain 'traceback' or 'unhandled' |

## Expected Final State

Result does not contain 'traceback' or 'unhandled'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
error_returned = true (not a crash)
no_pr_created = true
