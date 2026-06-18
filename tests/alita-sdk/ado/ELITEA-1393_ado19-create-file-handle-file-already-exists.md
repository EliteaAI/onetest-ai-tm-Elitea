---
id: ELITEA-1393
title: "ADO19 - create_file: Handle file already exists"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [negative-test, repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1393: ADO19 - create_file: Handle file already exists

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'create_file' tool handles duplicate file paths appropriately.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
File 'README.md' already exists on the 'main' branch.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `create_file` tool with file_path = 'README.md' (a file that already exists on the branch) | Tool executes but returns an error (continue_on_error is active) |
| 3 | Verify the response contains an error indicating the file already exists (e.g., 'already exists', 'exists', 'duplicate', 'conflict') | At least one expected error indicator present in the response |
| 4 | Verify the tool did not crash or throw an unhandled exception | Response does not contain 'traceback' or 'stack trace' |

## Expected Final State

Response does not contain 'traceback' or 'stack trace'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
error_about_existing_file = true
no_crash = true
