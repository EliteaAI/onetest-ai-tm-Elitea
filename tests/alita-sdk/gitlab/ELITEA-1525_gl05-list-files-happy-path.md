---
id: ELITEA-1525
title: "GL05 - List Files (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [list_files, gitlab, smoke, files]
requirements: []
---
# ELITEA-1525: GL05 - List Files (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Test list_files returns files from a branch: create branch, create three files (including one in a subdirectory), call list_files, verify all files are returned.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl05-list-files-<timestamp>
File 1: test/gl05_file1.txt
File 2: test/gl05_file2.txt
File 3: test/subdir/gl05_file3.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke create_branch to create a test branch | Test branch created |
| 3 | Invoke create_file to create first file (test/gl05_file1.txt) on the branch | First file created |
| 4 | Invoke create_file to create second file (test/gl05_file2.txt) on the branch | Second file created |
| 5 | Invoke create_file to create third file in subdirectory (test/subdir/gl05_file3.txt) on the branch | Third file created in subdirectory |
| 6 | Invoke list_files on the test branch | All three files returned in the listing |
| 7 | Validate all three file paths are present in the list_files response | All created files visible in listing |

## Expected Final State

All created files visible in listing

## Pass/Fail Criteria

All three create_file calls succeed
list_files returns at least the three created files
All tools complete without error
