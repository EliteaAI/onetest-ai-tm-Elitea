---
id: ELITEA-1450
title: "BB08 - List Files - Subdirectory"
priority: high
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [subdirectory, list_files, bitbucket, files]
requirements: []
---
# ELITEA-1450: BB08 - List Files - Subdirectory

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify the Bitbucket 'list_files' tool correctly lists files in a subdirectory. Tests path parameter navigation to subdirectory, recursive vs non-recursive listing, and validates file paths are correctly prefixed.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository has known stable subdirectory with files

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Test subdirectory: known stable subdirectory with files (defined in test YAML)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call list_files with a known stable subdirectory path and recursive=true | Recursive listing shows files in subdirectory and all nested subdirectories |
| 2 | Call list_files with the same subdirectory path and recursive=false | Non-recursive listing shows only direct children of the specified subdirectory |
| 3 | LLM validates: path parameter correctly navigated to subdirectory, recursive shows nested files, non-recursive shows only direct children, file paths are correctly prefixed with subdirectory path | Validation confirms subdirectory listing works correctly with path parameter |

## Expected Final State

Validation confirms subdirectory listing works correctly with path parameter

## Pass/Fail Criteria

PASS: Path parameter navigates to subdirectory, recursive returns nested files, non-recursive returns only direct children, paths correctly prefixed
FAIL: Empty subdirectory result, wrong path prefix, recursive = non-recursive content
