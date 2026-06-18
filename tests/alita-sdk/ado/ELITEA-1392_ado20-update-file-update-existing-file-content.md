---
id: ELITEA-1392
title: "ADO20 - update_file: Update existing file content"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1392: ADO20 - update_file: Update existing file content

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'update_file' tool updates an existing file's content.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
An existing file (e.g., 'README.md') is present on the target branch.
The test has write permissions to the branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `update_file` tool with an existing file_path, new content string, commit_message, and branch_name | Tool executes and returns a success response |
| 3 | Verify the update response contains a success indicator (e.g., commit ID or 'updated') | success_indicated = true |
| 4 | Call `read_file` to verify the file now contains the updated content | File content matches the newly provided content |
| 5 | Verify neither response contains 'error' or 'failed' | no_error = true |

## Expected Final State

no_error = true

## Pass/Fail Criteria

test_passed = true
tool_executed = true
success_indicated = true
content_updated = true
no_error = true
