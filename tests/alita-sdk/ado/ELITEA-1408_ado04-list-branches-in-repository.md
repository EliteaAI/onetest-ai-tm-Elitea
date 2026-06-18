---
id: ELITEA-1408
title: "ADO04 - List Branches in Repository"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1408: ADO04 - List Branches in Repository

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_branches_in_repo' tool retrieves branch list

## Preconditions

ADO Repos toolkit is configured with valid credentials.
ADO_REPOSITORY_ID is set.
Branch 'EliteaTest' exists in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with the target repository ID | Toolkit initialized successfully |
| 2 | Call `list_branches_in_repo` tool passing repository_id | Tool executes and returns a list of branches |
| 3 | Verify the result contains the 'EliteaTest' branch | Branch named 'EliteaTest' exists in the returned list |
| 4 | Verify no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
has_main = true (EliteaTest branch found)
