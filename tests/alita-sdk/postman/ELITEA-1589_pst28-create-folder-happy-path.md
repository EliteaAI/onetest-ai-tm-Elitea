---
id: ELITEA-1589
title: "PST28 - Create Folder (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [create_folder, folders, postman, smoke]
requirements: []
---
# ELITEA-1589: PST28 - Create Folder (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the create_folder tool successfully creates a new folder in the collection.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with write access
Folder name: AutoTestFolder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke create_folder with POSTMAN_COLLECTION_ID and a new folder name | Tool accepts parameters and creates folder at collection root |
| 3 | Capture the tool response and extract new folder path | Response contains new folder path in the collection |
| 4 | Delete the created folder to clean up | Cleanup successful |
| 5 | Validate LLM confirms folder was created in the collection | LLM confirms folder created at collection root |

## Expected Final State

LLM confirms folder created at collection root

## Pass/Fail Criteria

create_folder creates a new folder in collection root
Folder appears in collection structure
No exception raised
