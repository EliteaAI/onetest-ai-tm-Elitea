---
id: ELITEA-2730
title: "BitBucket - delete_file: Successfully removes file from non-default branch"
priority: critical
type: functional
module: bitbucket
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, bitbucket, file-operations, issue:3401]
requirements: [EliteaAI/elitea_issues#3401]
---
# ELITEA-2730: BitBucket - delete_file: Successfully removes file from non-default branch

**Module:** Bitbucket · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `delete_file` can remove files from branches other than default without affecting other branches.

## Preconditions

BitBucket toolkit configured with write/delete permissions.

## Test Data

| Parameter | Value |
|-----------|-------|
| file_path | "test-delete-feature.txt" |
| branch_name | "feature/test-delete" |
| commit_message | "Remove feature branch test file" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Create test branch "feature/test-delete" | Branch exists |
| 2 | Add test file "test-delete-feature.txt" to this branch | File exists in feature branch |
| 3 | Call `delete_file` with the test data parameters | Tool executes without errors |
| 4 | Check the feature branch | File is deleted from the feature branch |
| 5 | Check the default branch | Default branch is unaffected (file doesn't exist there or remains if it existed) |
| 6 | Check commit history | Commit appears only in the feature branch history |

## Expected Final State

File is deleted from feature branch only, default branch is unaffected, commit is created in feature branch.

## Pass/Fail Criteria

**Pass:**
- File is deleted from feature branch
- Default branch remains unaffected
- Commit created in feature branch only

**Fail:**
- File not deleted from feature branch
- Default branch is affected
- Commit appears in wrong branch or missing
