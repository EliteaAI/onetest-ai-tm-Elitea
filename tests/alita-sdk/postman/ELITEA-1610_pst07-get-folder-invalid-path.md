---
id: ELITEA-1610
title: "PST07 - Get Folder (Invalid Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [error-handling, get_folder, negative, folders, postman]
requirements: []
---
# ELITEA-1610: PST07 - Get Folder (Invalid Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_folder tool properly handles requests for non-existent or invalid folder paths, returning a descriptive error.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
NEGATIVE test — folder path used does not exist in the collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Invalid folder path: NonExistentFolder/SubFolder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_folder with POSTMAN_COLLECTION_ID and an invalid folder path (e.g., NonExistentFolder/SubFolder) | Tool attempts execution with the invalid path |
| 3 | Capture the tool response | Error returned indicating folder not found |
| 4 | Validate LLM confirms error was returned and no folder content retrieved | LLM confirms descriptive error returned without exception |

## Expected Final State

LLM confirms descriptive error returned without exception

## Pass/Fail Criteria

get_folder returns error for invalid path
Error message indicates folder not found
Tool exits cleanly
