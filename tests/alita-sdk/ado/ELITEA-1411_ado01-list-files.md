---
id: ELITEA-1411
title: "ADO01 - List Files"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [repository, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1411: ADO01 - List Files

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'list_files' tool retrieves files from repository root

## Preconditions

ADO Repos toolkit is configured with valid credentials and repository access.
ADO_REPOSITORY_ID environment variable is set.
Repository contains files: /ElitePipeline.yml and /README.md

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with repository ID | Toolkit is initialized and ready |
| 2 | Call `list_files` tool with path = '.' (repository root) | Tool executes without error and returns a list of file paths |
| 3 | Verify the returned file list contains '/ElitePipeline.yml' | '/ElitePipeline.yml' is present in the file list |
| 4 | Verify the returned file list contains '/README.md' | '/README.md' is present in the file list |
| 5 | Validate no error message or exception is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
found_expected = true
missing = []
