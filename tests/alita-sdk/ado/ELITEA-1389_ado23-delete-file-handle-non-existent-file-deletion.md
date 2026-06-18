---
id: ELITEA-1389
title: "ADO23 - delete_file: Handle non-existent file deletion"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [negative-test, repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1389: ADO23 - delete_file: Handle non-existent file deletion

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'delete_file' tool handles deletion of non-existent file appropriately.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
File 'non-existent-file-to-delete.txt' does NOT exist on the target branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `delete_file` tool with a non-existent file_path (e.g., 'non-existent-file-to-delete-{TIMESTAMP}.txt'), commit_message, and branch_name = 'main' | Tool executes but returns an error (continue_on_error is active, no crash) |
| 3 | Verify the response contains a file-not-found error indicator (e.g., 'not found', 'does not exist', '404', 'no such file') | At least one expected error indicator present in the response |
| 4 | Verify the pipeline continued execution (error was handled by continue_on_error) | Validation step was reached after the delete attempt |
| 5 | Verify the tool did not throw an unhandled exception | Response does not contain 'traceback' or 'stack trace' |

## Expected Final State

Response does not contain 'traceback' or 'stack trace'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
file_not_found_detected = true
handled_gracefully = true
