---
id: ELITEA-1451
title: "BB04 - Set Active Branch - Non-Existent Branch"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [set_active_branch, error-handling, bitbucket, negative, branch]
requirements: []
---
# ELITEA-1451: BB04 - Set Active Branch - Non-Existent Branch

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'set_active_branch' tool handles non-existent branch gracefully. Tests error handling for invalid branch name, returns appropriate error message including list of available branches.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
NEGATIVE test — expected outcome is error/graceful handling
Target branch does not exist in repository

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Invalid branch name: 'non-existent-branch-xyz-99999' (must not exist in repository)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call list_branches_in_repo to retrieve current available branches in repository | List of existing branches returned successfully |
| 2 | Call set_active_branch with a branch name that does not exist (e.g., 'non-existent-branch-xyz-99999') | Tool returns an error message indicating branch not found |
| 3 | LLM validates: error message is informative, includes indication of available branches or list of valid options, no unhandled exceptions | Validation confirms graceful error handling with helpful error message |

## Expected Final State

Validation confirms graceful error handling with helpful error message

## Pass/Fail Criteria

PASS: set_active_branch returns error message indicating branch not found, error includes helpful info, no exception
FAIL: Tool crashes/throws unhandled exception, misleading error message, creates branch unexpectedly
