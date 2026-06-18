---
id: ELITEA-1585
title: "PST30 - Update Folder (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_folder, folders, postman, smoke]
requirements: []
---
# ELITEA-1585: PST30 - Update Folder (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_folder tool successfully updates folder properties including name, description, and authentication.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
POSTMAN_FOLDER_PATH set to an existing folder path
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_FOLDER_PATH: path to an existing folder
New folder name: UpdatedFolderName

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_folder with POSTMAN_COLLECTION_ID, POSTMAN_FOLDER_PATH, and a new folder name | Tool accepts parameters and applies the rename |
| 3 | Capture the tool response and verify success | Tool confirms folder renamed without error |
| 4 | Validate LLM confirms folder was renamed | LLM confirms folder update applied |

## Expected Final State

LLM confirms folder update applied

## Pass/Fail Criteria

update_folder renames the target folder successfully
Folder name confirmed changed in collection
No exception raised
