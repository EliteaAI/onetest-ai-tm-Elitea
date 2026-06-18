---
id: ELITEA-1449
title: "BB05 - List Branches In Repo"
priority: critical
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [list_branches_in_repo, bitbucket, branch, smoke]
requirements: []
---
# ELITEA-1449: BB05 - List Branches In Repo

**Module:** Bitbucket · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Bitbucket 'list_branches_in_repo' tool retrieves branches from repository. Tests branch listing with and without limit parameter, validates default branch is present and branch names are properly formatted.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository has at least one branch (main/master)

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Expected default branch: 'main' or 'master'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call list_branches_in_repo without limit parameter to retrieve all branches | Full branch list returned containing at least one default branch (main/master) |
| 2 | Call list_branches_in_repo with limit=1 to test pagination/limit parameter | Exactly 1 branch returned in the limited result set |
| 3 | LLM validates: both calls succeed, default branch present in full listing, limit=1 returns exactly one branch, branch names are properly formatted | Validation confirms list_branches_in_repo functions correctly with and without limit |

## Expected Final State

Validation confirms list_branches_in_repo functions correctly with and without limit

## Pass/Fail Criteria

PASS: Full listing returns multiple branches containing default branch, limit=1 returns exactly 1 branch
FAIL: Empty branch list, default branch missing, limit not respected, incorrectly formatted names
