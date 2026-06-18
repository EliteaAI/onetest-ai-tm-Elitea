---
id: ELITEA-1402
title: "ADO10 - set_active_branch: Switch to existing branch"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1402: ADO10 - set_active_branch: Switch to existing branch

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'set_active_branch' tool successfully switches to an existing branch.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Branch 'EliteaTest' exists in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `set_active_branch` tool with branch_name = 'EliteaTest' | Tool executes without error |
| 3 | Verify the response confirms the active branch was switched to 'EliteaTest' | Response contains branch name 'EliteaTest' or a success confirmation |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
branch_switched = true
no_error = true
