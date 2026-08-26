---
id: ELITEA-2732
title: "BitBucket - delete_file: branch_name parameter targets correct branch"
priority: high
type: functional
module: bitbucket
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, bitbucket, file-operations, issue:3401]
requirements: [EliteaAI/elitea_issues#3401]
---
# ELITEA-2732: BitBucket - delete_file: branch_name parameter targets correct branch

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the `branch_name` parameter correctly targets specific branches and only affects the specified branch.

## Preconditions

BitBucket toolkit configured with write/delete permissions.

## Test Data

| Branch Name | Test File |
|-------------|-----------|
| "main" | "main-test.txt" |
| "develop" | "develop-test.txt" |
| "feature/delete-test" | "feature-test.txt" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Create file "main-test.txt" in "main" branch | File exists in main |
| 2 | Create file "develop-test.txt" in "develop" branch | File exists in develop |
| 3 | Create file "feature-test.txt" in "feature/delete-test" branch | File exists in feature branch |
| 4 | Call `delete_file` with file_path="main-test.txt", branch_name="main" | File deleted from main branch only |
| 5 | Verify "develop-test.txt" still exists in develop branch | File remains in develop |
| 6 | Verify "feature-test.txt" still exists in feature branch | File remains in feature branch |
| 7 | Call `delete_file` with file_path="develop-test.txt", branch_name="develop" | File deleted from develop branch only |
| 8 | Verify "feature-test.txt" still exists in feature branch | File remains in feature branch |
| 9 | Call `delete_file` with file_path="feature-test.txt", branch_name="feature/delete-test" | File deleted from feature branch only |

## Expected Final State

Each delete operation only affects the specified branch, leaving other branches intact.

## Pass/Fail Criteria

**Pass:**
- Each file is deleted from its specified branch only
- Other branches remain unaffected
- Branch parameter correctly targets the intended branch

**Fail:**
- Delete affects wrong branch
- Multiple branches are affected by a single delete
- Branch targeting does not work correctly
