---
id: ELITEA-1587
title: "PST29 - Create Folder (Nested)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [create_folder, folders, postman, nested]
requirements: []
---
# ELITEA-1587: PST29 - Create Folder (Nested)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the create_folder tool successfully creates a folder nested inside a parent folder using the parent_path parameter.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
A parent folder exists in the target collection
POSTMAN_FOLDER_PATH env var set to an existing folder path
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_FOLDER_PATH: path to an existing parent folder
New folder name: NestedAutoTestFolder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke create_folder with POSTMAN_COLLECTION_ID, a new folder name, and POSTMAN_FOLDER_PATH as parent | Tool accepts nested folder parameters |
| 3 | Capture the tool response and verify nested folder was created | Response confirms folder created under the specified parent path |
| 4 | Delete the created nested folder to clean up | Cleanup successful |
| 5 | Validate LLM confirms nested folder created under specified parent | LLM confirms nested folder creation succeeded |

## Expected Final State

LLM confirms nested folder creation succeeded

## Pass/Fail Criteria

create_folder with parent path creates nested folder
Folder appears as child of specified parent
No exception raised
