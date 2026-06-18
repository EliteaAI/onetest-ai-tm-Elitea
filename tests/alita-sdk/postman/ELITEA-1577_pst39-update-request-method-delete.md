---
id: ELITEA-1577
title: "PST39 - Update Request Method (DELETE)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_method, delete-method, requests, postman]
requirements: []
---
# ELITEA-1577: PST39 - Update Request Method (DELETE)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_method tool properly handles updating to various HTTP methods including DELETE.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
New method: DELETE

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_method with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and method=DELETE | Tool accepts DELETE method parameter |
| 3 | Capture the tool response | Tool confirms method updated to DELETE |
| 4 | Validate LLM confirms DELETE method applied to the request | LLM confirms method change to DELETE succeeded |

## Expected Final State

LLM confirms method change to DELETE succeeded

## Pass/Fail Criteria

update_request_method to DELETE accepted without error
Method confirmed as DELETE after update
No exception raised
