---
id: ELITEA-1396
title: "ADO16 - create_branch: Create new branch successfully"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1396: ADO16 - create_branch: Create new branch successfully

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'create_branch' tool creates a new branch from main.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
A unique branch name (e.g., 'test-branch-{TIMESTAMP}') does not yet exist in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `create_branch` tool with a unique branch_name (e.g., 'test-branch-{TIMESTAMP}') based off main | Tool executes and returns a success response |
| 3 | Verify the creation response contains a success indicator (e.g., 'created', 'refs/heads', or similar confirmation) | success_indicated = true |
| 4 | Call `list_branches_in_repo` to verify the new branch now exists | New branch name appears in the branch list |
| 5 | Verify neither response contains 'error' or 'failed' | no_error = true in both create and list responses |

## Expected Final State

no_error = true in both create and list responses

## Pass/Fail Criteria

test_passed = true
tool_executed = true
success_indicated = true
branch_exists_in_list = true
no_error = true
