---
id: ELITEA-1386
title: "ADO26 - list_branches_in_repo: Verify branch details"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1386: ADO26 - list_branches_in_repo: Verify branch details

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_branches_in_repo' tool returns branch details including commit info.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Repository contains at least branches: 'main' and 'EliteaTest'.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `list_branches_in_repo` tool with no additional parameters | Tool executes and returns a list of branches |
| 3 | Verify 'main' branch is present in the returned list | Branch named 'main' exists in results |
| 4 | Verify 'EliteaTest' branch is present in the returned list | Branch named 'EliteaTest' exists in results |
| 5 | Verify each branch entry includes commit metadata (commit ID, author, or date) | branches_have_commit_info = true |
| 6 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
has_main_branch = true
has_elitea_test_branch = true
branches_have_commit_info = true
no_error = true
