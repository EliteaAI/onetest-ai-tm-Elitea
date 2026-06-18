---
id: ELITEA-1578
title: "PST38 - Update Request Method (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_method, requests, postman, smoke]
requirements: []
---
# ELITEA-1578: PST38 - Update Request Method (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_method tool successfully updates the HTTP method of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing GET request
New method: POST

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_method with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and method=POST | Tool accepts method change parameters |
| 3 | Capture the tool response and verify method updated | Tool confirms method changed to POST |
| 4 | Validate LLM confirms method updated on the request | LLM confirms method change applied |

## Expected Final State

LLM confirms method change applied

## Pass/Fail Criteria

update_request_method changes HTTP method to specified value
Method confirmed updated in collection
No exception raised
