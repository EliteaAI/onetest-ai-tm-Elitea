---
id: ELITEA-1483
title: "FG05 - Get File Versions"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file_versions, versions, figma, file]
requirements: []
---
# ELITEA-1483: FG05 - Get File Versions

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Verify get_file_versions retrieves the version history of a Figma file, returning a list of versions with timestamps, user info, and version IDs.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Target file has at least one saved version

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key with version history

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a file with version history | Environment variable set |
| 3 | Invoke get_file_versions tool with file_key parameter | API request sent to Figma file versions endpoint |
| 4 | Validate response contains versions array | Versions list is present in response |
| 5 | Verify each version entry has id, created_at, and user fields | Version metadata is complete |
| 6 | Confirm at least one version is returned | File has version history accessible |

## Expected Final State

File has version history accessible

## Pass/Fail Criteria

Response contains versions array with at least one entry
Each version has id, created_at, user, and description fields
Pagination supported if many versions exist
Tool completes without error
