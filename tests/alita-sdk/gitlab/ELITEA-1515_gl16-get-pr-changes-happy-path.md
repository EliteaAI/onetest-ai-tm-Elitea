---
id: ELITEA-1515
title: "GL16 - Get PR Changes (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [get_pr_changes, merge-requests, gitlab, smoke]
requirements: []
---
# ELITEA-1515: GL16 - Get PR Changes (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify get_pr_changes retrieves file diffs for an existing merge request, returning the list of changed files with diff content.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
GITLAB_MR_IID env var set to an existing merge request IID with file changes

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
GITLAB_MR_IID: existing merge request IID that has file changes

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Set GITLAB_MR_IID to an existing merge request IID with file changes | MR IID ready |
| 3 | Invoke get_pr_changes with the MR IID | API request sent to GitLab MR changes endpoint |
| 4 | Validate response contains a list of changed files | Changes list returned with at least one file |
| 5 | Verify each change entry has a file path and diff content | File path and diff present for each changed file |

## Expected Final State

File path and diff present for each changed file

## Pass/Fail Criteria

get_pr_changes returns changes list for the specified MR IID
At least one file change entry is returned
Diff content is present for changed files
Tool completes without error
