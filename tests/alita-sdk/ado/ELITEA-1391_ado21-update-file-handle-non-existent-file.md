---
id: ELITEA-1391
title: "ADO21 - update_file: Handle non-existent file"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [negative-test, repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1391: ADO21 - update_file: Handle non-existent file

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'update_file' tool handles updating a non-existent file appropriately.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
File 'non-existent-file.txt' does NOT exist on the target branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `update_file` tool with a non-existent file_path (e.g., 'non-existent-file.txt'), some content, and commit_message | Tool executes but returns an error (continue_on_error is active) |
| 3 | Verify the response contains an error indicating the file was not found (e.g., 'not found', 'does not exist', '404') | At least one expected error indicator present in the response |
| 4 | Verify the tool did not crash or throw an unhandled exception | Response does not contain 'traceback' or 'stack trace' |

## Expected Final State

Response does not contain 'traceback' or 'stack trace'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
error_file_not_found = true
no_crash = true
