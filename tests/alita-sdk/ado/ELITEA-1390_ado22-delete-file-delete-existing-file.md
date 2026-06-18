---
id: ELITEA-1390
title: "ADO22 - delete_file: Delete existing file"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1390: ADO22 - delete_file: Delete existing file

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'delete_file' tool deletes an existing file from repository. NOTE: This test depends on ADO18 having created the file first.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
ADO18 (TC-0112) has run first and created the target file.
File exists on the target branch ready for deletion.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure prerequisite: ADO18 (TC-0112) has created the test file on the branch | Test file exists in the repository |
| 2 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 3 | Call `delete_file` tool with the file_path (created by ADO18), commit_message, and branch_name | Tool executes and returns a success response |
| 4 | Verify the deletion response contains a success indicator (e.g., commit ID or 'deleted') | success_indicated = true |
| 5 | Call `list_files` on the directory to verify the file no longer exists | Deleted file name is NOT present in the file list |
| 6 | Verify neither response contains 'error' or 'failed' | no_error = true |

## Expected Final State

no_error = true

## Pass/Fail Criteria

test_passed = true
tool_executed = true
success_indicated = true
file_not_in_list = true
no_error = true
