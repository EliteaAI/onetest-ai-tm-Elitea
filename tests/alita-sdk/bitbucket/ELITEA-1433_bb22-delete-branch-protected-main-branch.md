---
id: ELITEA-1433
title: "BB22 - Delete Branch - Protected Main Branch"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [delete_branch, protection, bitbucket, negative, branch]
requirements: []
---
# ELITEA-1433: BB22 - Delete Branch - Protected Main Branch

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'delete_branch' tool prevents deletion of the protected 'main' branch. Tests that attempting to delete 'main' fails, appropriate error message is returned indicating deletion is forbidden, and branch remains in repository.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
'main' branch exists in repository
NEGATIVE test — expected outcome is error/protection mechanism

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Target branch for deletion attempt: 'main' (protected default branch)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call list_branches_in_repo to confirm the 'main' branch exists in repository | 'main' branch present in branch listing |
| 2 | Call delete_branch targeting the 'main' branch | delete_branch returns error indicating deletion is forbidden or branch is protected |
| 3 | LLM validates: deletion attempt returned appropriate error message, error indicates branch is protected/deletion forbidden, no unhandled exceptions, 'main' branch should still exist | Validation confirms protection mechanism prevents deletion of the main branch |

## Expected Final State

Validation confirms protection mechanism prevents deletion of the main branch

## Pass/Fail Criteria

PASS: delete_branch returns error indicating deletion forbidden/protected for main branch, branch remains in repo
FAIL: Main branch deleted successfully, no error returned, unhandled exception
