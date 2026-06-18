---
id: ELITEA-1394
title: "ADO18 - create_file: Create new file in repository"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1394: ADO18 - create_file: Create new file in repository

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'create_file' tool creates a new file with content.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
The target branch exists (e.g., 'EliteaTest').
The file path to be created does not already exist on that branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `create_file` tool with a unique file_path (e.g., 'test-file-{TIMESTAMP}.txt'), file content, commit_message, and branch_name | Tool executes and returns a success response |
| 3 | Verify the creation response contains a success indicator (e.g., commit ID, 'created', or file metadata) | success_indicated = true |
| 4 | Call `list_files` on the target directory to verify the newly created file exists | New file appears in the directory listing |
| 5 | Verify neither response contains 'error' or 'failed' | no_error = true in both create and verify responses |

## Expected Final State

no_error = true in both create and verify responses

## Pass/Fail Criteria

test_passed = true
tool_executed = true
success_indicated = true
file_exists_in_list = true
no_error = true
