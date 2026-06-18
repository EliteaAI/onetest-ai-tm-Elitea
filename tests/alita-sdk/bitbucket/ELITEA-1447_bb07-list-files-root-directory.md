---
id: ELITEA-1447
title: "BB07 - List Files - Root Directory"
priority: critical
type: functional
module: bitbucket
status: ready
execution_type: automated
tags: [list_files, bitbucket, smoke, files]
requirements: []
---
# ELITEA-1447: BB07 - List Files - Root Directory

**Module:** Bitbucket · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Bitbucket 'list_files' tool lists files in repository root directory. Tests both recursive and non-recursive listing options, validates common root files are present (README, .gitignore, etc.) and output is properly structured.

## Preconditions

Bitbucket toolkit is configured and authenticated
BB_REPO and BB_WORKSPACE env vars are set
Repository has known files at root level (README, .gitignore, etc.)

## Test Data

BB_TOOLKIT_ID: Bitbucket toolkit ID
BB_TOOLKIT_NAME: Bitbucket toolkit name
BB_REPO: Target repository name
BB_WORKSPACE: Bitbucket workspace slug
Expected root files: README.md, .gitignore (or similar common root files)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call list_files at root directory ('/' or '') with recursive=true | Full recursive listing returned including files in all subdirectories |
| 2 | Call list_files at root directory with recursive=false (non-recursive) | Only root-level items returned (no subdirectory contents) |
| 3 | LLM validates: recursive listing contains more files than non-recursive, common root files present (README, .gitignore, etc.), output is properly structured | Validation confirms list_files works correctly for root directory with both recursive modes |

## Expected Final State

Validation confirms list_files works correctly for root directory with both recursive modes

## Pass/Fail Criteria

PASS: Recursive listing contains more files than non-recursive, both contain known root files (README, .gitignore), output is structured
FAIL: Empty listings, known root files missing, recursive = non-recursive count
