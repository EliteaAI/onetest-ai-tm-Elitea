---
id: ELITEA-1607
title: "PST08 - Get Request by Path (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_request_by_path, requests, postman, smoke]
requirements: []
---
# ELITEA-1607: PST08 - Get Request by Path (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_request_by_path tool successfully retrieves a specific API request using its path within the collection.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains a request at a known path
POSTMAN_REQUEST_PATH env var set to valid request path

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: valid path to existing request (e.g., Auth/Login)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_request_by_path with POSTMAN_COLLECTION_ID and a valid request path (e.g., FolderName/RequestName) | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains request details including method, URL, and name |
| 4 | Validate LLM confirms request was retrieved with expected fields | LLM confirms request details returned correctly |

## Expected Final State

LLM confirms request details returned correctly

## Pass/Fail Criteria

get_request_by_path returns request details
Request includes method, URL, and name
No exception raised
