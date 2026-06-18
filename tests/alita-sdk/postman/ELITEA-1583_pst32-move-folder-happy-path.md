---
id: ELITEA-1583
title: "PST32 - Move Folder (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [move_folder, folders, postman, smoke]
requirements: []
---
# ELITEA-1583: PST32 - Move Folder (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the move_folder tool successfully moves a folder to a different location within the collection hierarchy.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
POSTMAN_FOLDER_PATH set to an existing source folder
A target folder exists as destination
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Source folder path (POSTMAN_FOLDER_PATH): SourceFolder
Target folder path: ParentFolder/SourceFolder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke move_folder with POSTMAN_COLLECTION_ID, source POSTMAN_FOLDER_PATH, and a target folder path | Tool accepts parameters and moves the folder |
| 3 | Capture the tool response and verify success | Tool confirms folder moved to new location |
| 4 | Validate LLM confirms folder appears at new location | LLM confirms move operation succeeded |

## Expected Final State

LLM confirms move operation succeeded

## Pass/Fail Criteria

move_folder relocates folder to target path
Folder appears at new location in collection
No exception raised
