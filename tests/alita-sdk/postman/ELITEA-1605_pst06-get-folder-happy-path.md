---
id: ELITEA-1605
title: "PST06 - Get Folder (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_folder, folders, postman, smoke]
requirements: []
---
# ELITEA-1605: PST06 - Get Folder (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_folder tool successfully retrieves a specific folder in flattened format with path-based structure.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains a folder with at least one request
POSTMAN_FOLDER_PATH env var set to valid folder path

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_FOLDER_PATH: valid path to existing folder (e.g., Authentication)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_folder with POSTMAN_COLLECTION_ID and a valid POSTMAN_FOLDER_PATH | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains folder content in flattened format with request paths |
| 4 | Validate LLM confirms folder items returned with expected path structure | LLM confirms folder retrieved successfully |

## Expected Final State

LLM confirms folder retrieved successfully

## Pass/Fail Criteria

get_folder returns folder content in flattened format
Requests within folder are listed with paths
No exception raised
