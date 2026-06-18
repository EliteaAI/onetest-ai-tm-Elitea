---
id: ELITEA-1524
title: "GL06 - List Files Recursive"
priority: medium
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [list_files, recursive, gitlab, files]
requirements: []
---
# ELITEA-1524: GL06 - List Files Recursive

**Module:** Gitlab · **Priority:** Medium · **Type:** Functional

**Objective:** Verify list_files recursive flag: create branch with a nested file, call list_files non-recursively (should not see nested file in root), then recursively (should see it), clean up.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl06-recursive-<timestamp>
Nested file path: subdir/nested/gl06_file.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke create_branch to create a test branch | Test branch created |
| 3 | Invoke create_file to create a nested file at path subdir/nested/gl06_file.txt on the branch | Nested file created in subdirectory |
| 4 | Invoke list_files on root path non-recursively (recursive=false) | Only root-level items returned; nested file NOT visible at root |
| 5 | Invoke list_files recursively (recursive=true) | Nested file path included in recursive listing |
| 6 | Validate recursive result contains the full nested path and non-recursive does not | Recursive flag behavior confirmed |
| 7 | Invoke delete_branch to clean up | Test branch deleted |

## Expected Final State

Test branch deleted

## Pass/Fail Criteria

create_branch and create_file succeed
Non-recursive list_files returns only root-level items
Recursive list_files returns the nested file path
delete_branch succeeds
All tools complete without error
