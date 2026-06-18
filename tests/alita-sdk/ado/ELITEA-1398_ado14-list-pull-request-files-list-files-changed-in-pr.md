---
id: ELITEA-1398
title: "ADO14 - list_pull_request_files: List files changed in PR"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1398: ADO14 - list_pull_request_files: List files changed in PR

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_pull_request_files' tool lists files changed in a pull request.

## Preconditions

ADO Repos toolkit is configured with valid credentials.
PR #10 exists and contains at least 1 changed file.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `list_pull_request_files` tool with pull_request_id = '10' | Tool executes without error |
| 3 | Verify the response contains a list/array of changed files | Result is a non-empty list structure |
| 4 | Verify at least 1 file is returned (PR #10 has known changes) | file_count >= 1 |
| 5 | Verify each file entry contains a 'path' field | Path field present in every file entry |
| 6 | Verify each file entry contains a 'diff' field | Diff field present in every file entry |

## Expected Final State

Diff field present in every file entry

## Pass/Fail Criteria

test_passed = true
tool_executed = true
returns_list = true
file_count >= 1
files_have_required_fields = true (path and diff per entry)
no_error = true
