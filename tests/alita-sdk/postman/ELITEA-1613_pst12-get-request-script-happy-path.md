---
id: ELITEA-1613
title: "PST12 - Get Request Script (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_request_script, scripts, postman, smoke]
requirements: []
---
# ELITEA-1613: PST12 - Get Request Script (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_request_script tool successfully retrieves test script content from a specific request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains a request with test scripts
POSTMAN_REQUEST_PATH env var set to a request that has test scripts

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to request with test scripts
script_type: test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_request_script with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and script_type=test | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains the test script content as text |
| 4 | Validate LLM confirms script content is non-empty and represents valid JavaScript test code | LLM confirms test script retrieved successfully |

## Expected Final State

LLM confirms test script retrieved successfully

## Pass/Fail Criteria

get_request_script returns script content without error
Script text is non-empty for a request with test scripts
No exception raised
