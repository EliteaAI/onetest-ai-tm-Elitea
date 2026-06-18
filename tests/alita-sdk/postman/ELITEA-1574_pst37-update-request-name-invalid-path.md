---
id: ELITEA-1574
title: "PST37 - Update Request Name (Invalid Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_name, error-handling, negative, requests, postman]
requirements: []
---
# ELITEA-1574: PST37 - Update Request Name (Invalid Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_name tool properly handles attempts to update a request that does not exist or has an invalid path.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Target request path does not exist

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Invalid request path: FakeFolder/NonExistentRequest

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_name with POSTMAN_COLLECTION_ID and a request path that does not exist | Tool attempts operation with invalid path |
| 3 | Capture the tool response | Response contains an error indicating request not found |
| 4 | Validate LLM confirms informative error returned | LLM confirms error message without crash |

## Expected Final State

LLM confirms error message without crash

## Pass/Fail Criteria

update_request_name with non-existent request path returns clear error
Error indicates request not found
No unhandled exception
