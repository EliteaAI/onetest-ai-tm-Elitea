---
id: ELITEA-1582
title: "PST31 - Update Folder (Invalid Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [error-handling, update_folder, negative, folders, postman]
requirements: []
---
# ELITEA-1582: PST31 - Update Folder (Invalid Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_folder tool properly handles attempts to update a folder that does not exist or has an invalid path.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Target path does not exist in the collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Invalid folder path: NonExistentFolder/AlsoMissing

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_folder with POSTMAN_COLLECTION_ID and a folder path that does not exist | Tool attempts operation with invalid path |
| 3 | Capture the tool response | Response contains an error indicating folder not found |
| 4 | Validate LLM confirms error was returned without crash | LLM confirms informative error message returned |

## Expected Final State

LLM confirms informative error message returned

## Pass/Fail Criteria

update_folder with non-existent path returns clear error message
Error indicates folder not found
No unhandled exception
