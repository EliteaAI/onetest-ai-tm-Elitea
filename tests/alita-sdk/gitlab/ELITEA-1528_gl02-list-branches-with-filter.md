---
id: ELITEA-1528
title: "GL02 - List Branches with Filter"
priority: medium
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [list_branches_in_repo, wildcard, branches, gitlab, filter]
requirements: []
---
# ELITEA-1528: GL02 - List Branches with Filter

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Test list_branches_in_repo wildcard filtering: create two test branches with a common prefix, list with wildcard filter, verify only matching branches returned, then clean up.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository (branch creation)

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch prefix: test/gl02-filter-<timestamp>
Branch 1: test/gl02-filter-a-<timestamp>
Branch 2: test/gl02-filter-b-<timestamp>
Wildcard filter: test/gl02-filter-*

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Generate two unique branch names with a common prefix (e.g., test/gl02-filter-a-<ts>, test/gl02-filter-b-<ts>) | Unique branch names generated |
| 3 | Invoke create_branch to create the first test branch | First branch created successfully |
| 4 | Invoke create_branch to create the second test branch | Second branch created successfully |
| 5 | Invoke list_branches_in_repo with wildcard filter matching the common prefix (e.g., test/gl02-filter-*) | Only branches matching the wildcard pattern are returned |
| 6 | Validate that both test branches appear in the filtered results and non-matching branches do not | Filter correctly scopes results to matching branches only |
| 7 | Invoke delete_branch to remove the first test branch | First branch deleted |
| 8 | Invoke delete_branch to remove the second test branch | Second branch deleted, repository cleaned up |

## Expected Final State

Second branch deleted, repository cleaned up

## Pass/Fail Criteria

create_branch succeeds for both test branches
list_branches_in_repo with wildcard filter returns only branches matching the pattern
delete_branch succeeds for both test branches
All tools complete without error
