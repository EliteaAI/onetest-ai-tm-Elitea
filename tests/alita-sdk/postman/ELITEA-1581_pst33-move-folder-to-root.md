---
id: ELITEA-1581
title: "PST33 - Move Folder to Root"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [move_folder, edge-case, folders, postman]
requirements: []
---
# ELITEA-1581: PST33 - Move Folder to Root

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the move_folder tool can move a folder to the root level of the collection by setting target_path to null or empty.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
POSTMAN_FOLDER_PATH set to a nested folder
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Nested source folder path (POSTMAN_FOLDER_PATH): ParentFolder/NestedFolder
Target path: (root / empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke move_folder with POSTMAN_COLLECTION_ID, nested POSTMAN_FOLDER_PATH, and empty/null target path to indicate root | Tool accepts root target parameter |
| 3 | Capture the tool response and verify folder moved to root | Tool confirms folder moved to collection root |
| 4 | Validate LLM confirms folder is now at collection root | LLM confirms move to root succeeded |

## Expected Final State

LLM confirms move to root succeeded

## Pass/Fail Criteria

move_folder to root moves folder out of all parent folders
Folder appears at collection root after operation
No exception raised
