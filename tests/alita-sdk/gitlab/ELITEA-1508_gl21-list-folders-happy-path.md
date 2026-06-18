---
id: ELITEA-1508
title: "GL21 - List Folders (Happy Path)"
priority: high
type: functional
module: gitlab
status: ready
execution_type: automated
tags: [list_folders, gitlab, files]
requirements: []
---
# ELITEA-1508: GL21 - List Folders (Happy Path)

**Module:** Gitlab · **Priority:** High · **Type:** Functional

**Objective:** Verify list_folders returns directory entries from the repository: create branch, create files in a nested directory structure, call list_folders to verify folder entries are returned.

## Preconditions

GitLab toolkit is configured and authenticated
GITLAB_TOOLKIT_NAME env var is set
Write access to repository

## Test Data

GITLAB_TOOLKIT_NAME: configured GitLab toolkit name
Branch name: test/gl21-list-folders-<timestamp>
Nested file path: folderA/folderB/gl21_file.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitLab toolkit and set GITLAB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke create_branch to create a test branch | Test branch created |
| 3 | Invoke create_file to create a file at a nested path (e.g., folderA/folderB/gl21_file.txt) | Nested directory structure created with file |
| 4 | Invoke list_folders on the test branch | Directory/folder entries returned |
| 5 | Validate that folderA appears in the list_folders results | Subdirectory created via file is visible as a folder |

## Expected Final State

Subdirectory created via file is visible as a folder

## Pass/Fail Criteria

create_branch and create_file succeed
list_folders returns at least one folder/directory entry
Created subfolder path present in results
Tool completes without error
