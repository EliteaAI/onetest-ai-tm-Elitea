---
id: ELITEA-1488
title: "FG03 - Get File (Happy Path)"
priority: critical
type: functional
module: figma
status: ready
execution_type: automated
tags: [get_file, smoke, figma, file]
requirements: []
---
# ELITEA-1488: FG03 - Get File (Happy Path)

**Module:** Figma · **Priority:** Critical · **Type:** Functional

**Objective:** Verify get_file retrieves the complete Figma file structure including document, components, styles, and page data.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID and FIGMA_FILE_KEY env vars are set
Target Figma file is accessible

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
FIGMA_FILE_KEY: valid Figma file key for a file with content

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token and set FIGMA_TOOLKIT_ID | Toolkit authenticated |
| 2 | Set FIGMA_FILE_KEY to a valid Figma file key | Environment variable set |
| 3 | Invoke get_file tool with file_key parameter | API request sent to Figma files endpoint |
| 4 | Validate response contains document object with pages array | Document structure is present and properly nested |
| 5 | Verify file name, key, and lastModified fields are present in response | File metadata is complete |
| 6 | Confirm styles and components dictionaries are included in response | Design system data retrieved successfully |

## Expected Final State

Design system data retrieved successfully

## Pass/Fail Criteria

Response contains document object with pages array
File name and key present in response
Styles and components fields included
Last modified timestamp present
Tool completes without error
