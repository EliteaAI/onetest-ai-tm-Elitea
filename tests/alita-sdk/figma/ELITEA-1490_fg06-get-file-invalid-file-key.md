---
id: ELITEA-1490
title: "FG06 - Get File (Invalid File Key)"
priority: high
type: functional
module: figma
status: ready
execution_type: automated
tags: [error-handling, negative, get_file, figma, file]
requirements: []
---
# ELITEA-1490: FG06 - Get File (Invalid File Key)

**Module:** Figma · **Priority:** High · **Type:** Functional

**Objective:** Test get_file error handling with an invalid file key, verifying the tool returns an appropriate error message rather than crashing.

## Preconditions

Figma toolkit is configured and authenticated
FIGMA_TOOLKIT_ID env var is set
NEGATIVE test — file key used is invalid or non-existent

## Test Data

FIGMA_TOOLKIT_ID: configured Figma toolkit ID
Invalid file key used: "INVALID_FILE_KEY_12345" (does not correspond to any real file)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Figma toolkit with valid API token | Toolkit authenticated |
| 2 | Use an invalid file key (e.g., "INVALID_KEY_00001") as the file_key parameter | Invalid key prepared |
| 3 | Invoke get_file tool with the invalid file_key | API request sent with invalid key |
| 4 | Validate response contains an error message (404 not found or 403 forbidden) | Error message returned indicating file does not exist or is inaccessible |
| 5 | Confirm no stack trace or unhandled exception is raised | Tool exits cleanly with error handled |

## Expected Final State

Tool exits cleanly with error handled

## Pass/Fail Criteria

Tool returns error message indicating file not found or access denied
No unhandled Python exception or stack trace
Error message is descriptive and actionable
