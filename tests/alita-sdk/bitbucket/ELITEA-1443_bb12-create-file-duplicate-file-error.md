---
id: ELITEA-1443
title: "BB12 - Create File - Duplicate File Error"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [error-handling, create_file, bitbucket, negative, files]
requirements: []
---
# ELITEA-1443: BB12 - Create File - Duplicate File Error

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'create_file' tool handles duplicate file creation gracefully. Tests that first creation succeeds, second creation fails with appropriate error, and original content is preserved (not overwritten).

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository is accessible with write permissions
NEGATIVE test — expected outcome is error on second creation

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Test file path: 'test/duplicate-file-{timestamp}.txt'
Original content: 'This is the original content - first creation'
Duplicate content attempt: 'This should NOT overwrite - second creation'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_branch to create a test branch for isolation | Test branch created successfully |
| 2 | Call create_file on test branch with initial content (first creation) | File created successfully |
| 3 | Call create_file on same path with different content (second creation - duplicate) | Second creation returns error indicating file already exists |
| 4 | Call read_file to verify the file still contains the original content | File content matches original content from first creation, NOT the second attempt content |
| 5 | LLM validates: first creation succeeded, second creation failed with appropriate error, original content preserved (not overwritten) | Validation confirms duplicate file handling works correctly |
| 6 | Cleanup: call delete_branch to remove the test branch | Test branch deleted, repository returned to clean state |

## Expected Final State

Test branch deleted, repository returned to clean state

## Pass/Fail Criteria

PASS: Second creation returns error indicating file exists, read_file returns original content unchanged
FAIL: Second creation silently overwrites file, no error on duplicate, original content changed
