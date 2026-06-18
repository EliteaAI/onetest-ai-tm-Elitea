---
id: ELITEA-1441
title: "BB14 - Update File - Invalid Markers"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [error-handling, update_file, bitbucket, negative, files]
requirements: []
---
# ELITEA-1441: BB14 - Update File - Invalid Markers

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'update_file' tool handles invalid markers gracefully. Tests that non-matching OLD content causes failure, missing NEW marker causes failure, original file content is preserved, and appropriate error messages are returned.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository is accessible with write permissions
NEGATIVE test — expected outcome is error on invalid marker syntax

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Test file content: 'Hello World - original content'
Invalid OLD marker: 'THIS_TEXT_DOES_NOT_EXIST_IN_FILE'
Malformed syntax: update without NEW marker delimiter

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call create_branch to create a test branch for isolation | Test branch created successfully |
| 2 | Call create_file on test branch with known content | File created successfully with initial content |
| 3 | Call update_file with OLD marker text that does NOT exist in the file (non-matching old content) | update_file returns error indicating OLD content not found in file |
| 4 | Call update_file with malformed marker syntax (missing NEW marker delimiter) | update_file returns error indicating invalid marker syntax |
| 5 | Call read_file to verify original content is preserved after both failed updates | File content exactly matches original content, no changes applied |
| 6 | Cleanup: call delete_branch to remove the test branch | Test branch deleted, repository returned to clean state |
| 7 | LLM validates: both invalid updates returned errors, original content preserved, graceful error handling | Validation confirms update_file handles invalid markers correctly without corrupting file |

## Expected Final State

Validation confirms update_file handles invalid markers correctly without corrupting file

## Pass/Fail Criteria

PASS: Both invalid update attempts return errors, read_file confirms original content preserved
FAIL: Invalid update silently succeeds, file content corrupted, no error returned
