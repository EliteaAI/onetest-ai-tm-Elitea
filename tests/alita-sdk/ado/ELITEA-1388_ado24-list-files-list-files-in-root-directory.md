---
id: ELITEA-1388
title: "ADO24 - list_files: List files in root directory"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1388: ADO24 - list_files: List files in root directory

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_files' tool can list files in the repository root directory.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Repository root directory contains at least one file.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `list_files` tool with directory_path = '' (empty string = root directory) | Tool executes without error |
| 3 | Verify the response contains a list or array of file paths | returns_list = true |
| 4 | Verify at least some files are returned from the root directory | file_count > 0 |
| 5 | Validate no error message is present in the result | Result does not contain 'error', 'failed', 'exception' |

## Expected Final State

Result does not contain 'error', 'failed', 'exception'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
returns_list = true
has_files = true (file_count > 0)
no_error = true
