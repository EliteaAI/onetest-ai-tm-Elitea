---
id: ELITEA-2729
title: "BitBucket - delete_file: Successfully removes file from default branch"
priority: critical
type: functional
module: bitbucket
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, bitbucket, file-operations, issue:3401]
requirements: [EliteaAI/elitea_issues#3401]
---
# ELITEA-2729: BitBucket - delete_file: Successfully removes file from default branch

**Module:** Bitbucket · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `delete_file` successfully removes a file from the repository's default branch with all required parameters.

## Preconditions

BitBucket toolkit configured with write/delete permissions.

## Test Data

| Parameter | Value |
|-----------|-------|
| file_path | "test-delete-main.txt" |
| branch_name | "main" (or default branch name) |
| commit_message | "Remove test file" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Create test file "test-delete-main.txt" in the default branch | File exists in repository |
| 2 | Call `delete_file` with the test data parameters | Tool executes without errors |
| 3 | Check the repository | File is deleted from the repository |
| 4 | Check commit history | A commit was created with message "Remove test file" |
| 5 | Call `list_files` on the branch | "test-delete-main.txt" no longer appears in the file list |

## Expected Final State

File is deleted, commit is created with the specified message, and file does not appear in list_files output.

## Pass/Fail Criteria

**Pass:**
- Tool executes without errors
- File is successfully deleted from repository
- Commit created with correct message
- File no longer in list_files output

**Fail:**
- Tool returns an error
- File still exists in repository
- No commit created or incorrect commit message
- File still appears in list_files
