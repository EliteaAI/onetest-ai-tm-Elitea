---
id: ELITEA-1576
title: "PST43 - Update Request Description (Clear)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_description, edge-case, requests, postman]
requirements: []
---
# ELITEA-1576: PST43 - Update Request Description (Clear)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_description tool properly handles clearing the request description by setting it to empty string.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Request has an existing description
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to a request with a description
Description: (empty string)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_description with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and an empty string | Tool accepts empty description |
| 3 | Capture the tool response | Tool confirms description cleared without error |
| 4 | Validate LLM confirms description cleared on the request | LLM confirms empty description applied |

## Expected Final State

LLM confirms empty description applied

## Pass/Fail Criteria

update_request_description with empty string clears the description
Description confirmed empty after operation
No exception raised
