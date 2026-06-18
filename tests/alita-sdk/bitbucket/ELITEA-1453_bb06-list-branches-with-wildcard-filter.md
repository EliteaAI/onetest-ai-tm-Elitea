---
id: ELITEA-1453
title: "BB06 - List Branches With Wildcard Filter"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [list_branches_in_repo, bitbucket, wildcard, branch]
requirements: []
---
# ELITEA-1453: BB06 - List Branches With Wildcard Filter

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'list_branches_in_repo' tool correctly filters branches using wildcards. Creates 3 test branches, then tests wildcard pattern filtering to ensure matching branches are included and non-matching branches are excluded.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository is accessible with write permissions

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Matching branches: 'test-wildcard-filter-1', 'test-wildcard-filter-2'
Non-matching branch: 'other-nonmatching-branch'
Wildcard pattern: 'test-wildcard-filter-*'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_branch to create test branch 1 (name matching wildcard, e.g., 'test-wildcard-filter-1') | Branch 1 created successfully |
| 2 | Call create_branch to create test branch 2 (name matching wildcard, e.g., 'test-wildcard-filter-2') | Branch 2 created successfully |
| 3 | Call create_branch to create test branch 3 (name NOT matching wildcard, e.g., 'other-nonmatching-branch') | Branch 3 created successfully |
| 4 | Call list_branches_in_repo with wildcard pattern 'test-wildcard-filter-*' to filter branches | Only branches matching pattern returned (branches 1 and 2), branch 3 excluded |
| 5 | Call list_branches_in_repo without filter to verify all 3 test branches exist before cleanup | All 3 test branches present in unfiltered listing |
| 6 | LLM validates: filtered listing contains only matching branches, non-matching branch excluded | Validation confirms wildcard filtering works correctly |
| 7 | Cleanup: call delete_branch for each of the 3 test branches | All 3 test branches deleted, repository returned to clean state |

## Expected Final State

All 3 test branches deleted, repository returned to clean state

## Pass/Fail Criteria

PASS: Filtered listing contains only the 2 matching branches, non-matching branch excluded
FAIL: Non-matching branch appears in filtered results, matching branches excluded, no filtering applied
