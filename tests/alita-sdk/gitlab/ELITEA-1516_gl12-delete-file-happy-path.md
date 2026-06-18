---
id: ELITEA-1516
title: "GL12 - Delete File (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [delete_file, gitlab, files]
requirements: []
---
# ELITEA-1516: GL12 - Delete File (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test delete_file removes a file from a branch: create branch, create file, delete file, verify it no longer exists, then clean up branch.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl12-delete-file-<timestamp>
File path: test/gl12_to_delete.txt
File content: "This file will be deleted by GL12 test"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke create_branch to create a test branch | Test branch created |
| 3 | Invoke create_file to create a test file on the branch | File created on branch |
| 4 | Invoke delete_file specifying the file path and branch | File deleted from branch |
| 5 | Invoke read_file to confirm the file no longer exists | read_file returns not found error for the deleted file |
| 6 | Invoke delete_branch to clean up the test branch | Test branch deleted |

## Expected Final State

Test branch deleted

## Pass/Fail Criteria

create_branch and create_file succeed
delete_file completes without error
read_file after deletion returns not found error
delete_branch succeeds
