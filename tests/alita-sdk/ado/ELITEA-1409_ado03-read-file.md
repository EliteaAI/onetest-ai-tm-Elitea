---
id: ELITEA-1409
title: "ADO03 - Read File"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1409: ADO03 - Read File

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'read_file' tool retrieves file content

## Preconditions

ADO Repos toolkit is configured with valid credentials.
File 'README.md' exists on the 'main' branch of the repository.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `read_file` tool with file_path = 'README.md' and branch = 'main' | Tool executes without error |
| 3 | Verify the returned content is non-empty | Content string has length > 0 |
| 4 | Verify the content contains a markdown heading (line starting with '#') | contains_heading = true |

## Expected Final State

contains_heading = true

## Pass/Fail Criteria

test_passed = true
tool_executed = true
contains_heading = true
