---
id: ELITEA-1608
title: "PST13 - Get Request Script (Pre-Request)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_request_script, prerequest, scripts, postman]
requirements: []
---
# ELITEA-1608: PST13 - Get Request Script (Pre-Request)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the get_request_script tool successfully retrieves pre-request script content when script_type is set to prerequest.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains a request with pre-request scripts
POSTMAN_REQUEST_PATH env var set to a request that has pre-request scripts

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to request with pre-request scripts
script_type: prerequest

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_request_script with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and script_type=prerequest | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains the pre-request script content as text |
| 4 | Validate LLM confirms pre-request script content returned and is valid JavaScript | LLM confirms pre-request script retrieved successfully |

## Expected Final State

LLM confirms pre-request script retrieved successfully

## Pass/Fail Criteria

get_request_script with prerequest type returns pre-request script content
Script text is non-empty
No exception raised
