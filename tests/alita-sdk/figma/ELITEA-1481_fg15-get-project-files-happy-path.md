---
id: ELITEA-1481
title: "FG15 - Get Project Files (Happy Path)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_project_files, projects, smoke, figma]
requirements: []
---
# ELITEA-1481: FG15 - Get Project Files (Happy Path)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Verify get_project_files retrieves all files in a Figma project, returning a list of files with keys, names, and metadata.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_PROJECT_ID env vars are set
Project contains at least one file

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_PROJECT_ID: valid Figma project ID with at least one file

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_PROJECT_ID to a valid Figma project ID | Environment variable set |
| 3 | Invoke get_project_files tool with project_id parameter | API request sent to Figma project files endpoint |
| 4 | Validate response contains list of file objects | Files list returned |
| 5 | Verify each file has key and name fields | File metadata is complete |
| 6 | Confirm at least one file is returned for the project | Project contains accessible files |

## Expected Final State

Project contains accessible files

## Pass/Fail Criteria

Files list returned for the specified project
Each file has key and name fields
At least one file present
Tool completes without error
