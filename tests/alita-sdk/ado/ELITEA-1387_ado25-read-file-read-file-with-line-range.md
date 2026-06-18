---
id: ELITEA-1387
title: "ADO25 - read_file: Read file with line range"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1387: ADO25 - read_file: Read file with line range

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'read_file' tool can read a specific line range from a file.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
File 'README.md' exists on the 'main' branch and has more than 10 lines.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `read_file` tool with file_path = 'README.md', branch = 'main', offset = 1, limit = 10 | Tool executes without error |
| 3 | Verify the returned content is non-empty | Content string has length > 0 |
| 4 | Verify the content length/line count indicates only ~10 lines were returned (not the entire file) | content_reasonable_length = true (approximate_line_count ≈ 10) |
| 5 | Validate no error message is present in the result | Result does not contain 'error', 'failed', 'not found' |

## Expected Final State

Result does not contain 'error', 'failed', 'not found'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
has_content = true
content_reasonable_length = true (not the entire file)
no_error = true
