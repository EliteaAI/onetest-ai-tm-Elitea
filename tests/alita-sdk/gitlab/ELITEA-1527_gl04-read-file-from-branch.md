---
id: ELITEA-1527
title: "GL04 - Read File from Branch"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [read_file, gitlab, branch, files]
requirements: []
---
# ELITEA-1527: GL04 - Read File from Branch

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify read_file can retrieve a file from a specific non-default branch: create branch, create file on that branch, read file specifying the branch, validate content, clean up.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl04-branch-read-<timestamp>
File path: test/gl04_branch_file.txt
File content: "Branch-specific content for GL04 test"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Generate unique branch name and file path | Unique names generated |
| 3 | Invoke create_branch to create a test branch | Test branch created |
| 4 | Invoke create_file on the test branch with content | File created on the specific branch (not on main) |
| 5 | Invoke read_file specifying both the file path and the test branch name | File content returned from the specific branch |
| 6 | Validate content matches what was written on that branch | Branch-specific file content verified |
| 7 | Attempt to read the same file path from main branch to confirm isolation | File not found on main branch (branch isolation confirmed) |
| 8 | Invoke delete_branch to clean up | Test branch deleted |

## Expected Final State

Test branch deleted

## Pass/Fail Criteria

create_branch succeeds
create_file creates file on the branch
read_file with branch_name parameter returns matching content
File not present on main branch (branch isolation confirmed)
delete_branch succeeds
