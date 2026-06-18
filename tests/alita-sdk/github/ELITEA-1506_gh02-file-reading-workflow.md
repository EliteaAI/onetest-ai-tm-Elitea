---
id: ELITEA-1506
title: "GH02 - File Reading Workflow"
priority: high
type: functional
module: github
status: ready
execution_type: automated
tags: [list_files, read_file, github, smoke, files]
requirements: []
---
# ELITEA-1506: GH02 - File Reading Workflow

**Module:** Github · **Priority:** High · **Type:** Functional

**Objective:** Test file reading operations: list files in branch, get files from directory, then read specific file content to verify each tool works in sequence.

## Preconditions

GitHub toolkit is configured and authenticated
GITHUB_TOOLKIT_NAME env var is set
Target repository has files in the main branch including a known directory

## Test Data

GITHUB_TOOLKIT_NAME: configured GitHub toolkit name
GITHUB_REPO: target repository
Directory path: a known directory in the repo (e.g., "alita_sdk/tools")
File paths: two known file paths in the repository

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure GitHub toolkit and set GITHUB_TOOLKIT_NAME | Toolkit authenticated |
| 2 | Invoke list_files_in_main_branch to retrieve the list of files in the main branch | Files list returned with at least one file |
| 3 | Invoke get_files_from_directory with a known directory path from the repository | Directory contents returned listing files in that path |
| 4 | Invoke read_file with a specific file path to retrieve file contents | File content returned as text string |
| 5 | Invoke read_file again with a second file path for additional verification | Second file content returned correctly |
| 6 | Validate LLM confirms all four tool responses indicate success | All file reading operations confirmed successful |

## Expected Final State

All file reading operations confirmed successful

## Pass/Fail Criteria

list_files_in_main_branch returns non-empty file list
get_files_from_directory returns files for target directory
read_file returns actual file content
All four tool calls succeed without error
