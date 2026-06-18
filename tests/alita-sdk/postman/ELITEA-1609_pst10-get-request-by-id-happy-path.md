---
id: ELITEA-1609
title: "PST10 - Get Request by ID (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_request_by_id, requests, postman, smoke]
requirements: []
---
# ELITEA-1609: PST10 - Get Request by ID (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_request_by_id tool successfully retrieves a specific API request using its unique identifier.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
POSTMAN_REQUEST_ID env var set to a valid request ID within the collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_ID: valid request ID within the collection

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_request_by_id with POSTMAN_COLLECTION_ID and POSTMAN_REQUEST_ID | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains full request details including method, URL, and name |
| 4 | Validate LLM confirms request returned matches the expected ID and structure | LLM confirms request details retrieved correctly |

## Expected Final State

LLM confirms request details retrieved correctly

## Pass/Fail Criteria

get_request_by_id returns request details with correct ID
Request includes method, URL, and headers
No exception raised
