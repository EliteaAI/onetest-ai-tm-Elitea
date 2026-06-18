---
id: ELITEA-1584
title: "PST34 - Create Request (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [create_request, requests, postman, smoke]
requirements: []
---
# ELITEA-1584: PST34 - Create Request (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the create_request tool successfully creates a new API request in a folder with basic properties.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
POSTMAN_FOLDER_PATH set to an existing folder in the collection
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_FOLDER_PATH: path to an existing folder
Request name: Auto GET Request
Method: GET
URL: https://httpbin.org/get

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke create_request with POSTMAN_COLLECTION_ID, POSTMAN_FOLDER_PATH, request name, method=GET, and URL | Tool accepts parameters and creates the request |
| 3 | Capture the tool response and extract request ID | Response contains new request ID and path confirmation |
| 4 | Delete the created request to clean up | Cleanup successful |
| 5 | Validate LLM confirms request was created successfully | LLM confirms GET request created in the specified folder |

## Expected Final State

LLM confirms GET request created in the specified folder

## Pass/Fail Criteria

create_request creates new GET request at specified folder path
Request appears in collection structure
No exception raised
