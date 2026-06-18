---
id: ELITEA-1395
title: "ADO17 - create_branch: Handle duplicate branch name"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [negative-test, repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1395: ADO17 - create_branch: Handle duplicate branch name

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'create_branch' tool handles duplicate branch names appropriately.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Branch 'main' already exists in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `create_branch` tool with branch_name = 'main' (an already-existing branch) | Tool executes but returns an error (continue_on_error is active) |
| 3 | Verify the response contains a duplicate-branch error indicator (e.g., 'already exists', 'exists', 'duplicate', 'error') | At least one expected error indicator is present in the response |
| 4 | Verify the tool did not crash or throw an unhandled exception | Response does not contain 'traceback' or 'stack trace' |

## Expected Final State

Response does not contain 'traceback' or 'stack trace'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
error_about_duplicate = true (contains 'already exists' or similar)
no_crash = true
