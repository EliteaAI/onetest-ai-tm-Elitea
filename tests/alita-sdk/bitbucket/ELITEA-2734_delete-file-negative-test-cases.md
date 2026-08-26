---
id: ELITEA-2734
title: "BitBucket - delete_file: negative test cases"
priority: high
type: functional
module: bitbucket
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, bitbucket, file-operations, issue:3401]
requirements: [EliteaAI/elitea_issues#3401]
---
# ELITEA-2734: BitBucket - delete_file: negative test cases

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify `delete_file` fails gracefully — no crash, no misleading success — for invalid input.

## Preconditions

BitBucket toolkit configured.

## Test Data

| Scenario | Input | Expected Result |
|----------|-------|-----------------|
| File not found | file_path="non-existent.txt", branch="main" | ToolException: "File not found" |
| Branch not found | file_path="test.txt", branch="invalid-branch" | ToolException: "Branch does not exist" |
| Empty file path | file_path="", branch="main" | ToolException: "File path is required" |
| Empty branch name | file_path="test.txt", branch="" | ToolException: "Branch name is required" |
| Insufficient permissions | Valid params, read-only credentials | ToolException: "Permission denied" or "Access denied" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `delete_file` with file_path="non-existent.txt", branch_name="main" | Returns ToolException with "File not found" message, no crash |
| 2 | Verify no commits created | Repository history is unchanged |
| 3 | Call `delete_file` with file_path="test.txt", branch_name="invalid-branch" | Returns ToolException with "Branch does not exist" message |
| 4 | Call `delete_file` with file_path="", branch_name="main" | Returns ToolException with "File path is required" message |
| 5 | Call `delete_file` with file_path="test.txt", branch_name="" | Returns ToolException with "Branch name is required" message |
| 6 | Configure toolkit with read-only credentials | Credentials have no delete permission |
| 7 | Call `delete_file` with valid parameters | Returns ToolException with "Permission denied" or "Access denied" message |
| 8 | Verify file still exists in repository | No files are affected |

## Expected Final State

Every invalid scenario is handled gracefully with clear ToolException — never a crash or misleading success.

## Pass/Fail Criteria

**Pass:**
- Every invalid scenario returns a clear ToolException
- Error messages match expected results
- No crashes or unhandled exceptions
- No unintended commits or file changes

**Fail:**
- Any scenario crashes the tool or hangs
- Error messages are unclear or misleading
- Invalid operations succeed without error
- Unintended commits or file changes occur
