---
id: ELITEA-1606
title: "PST09 - Get Request by Path (Invalid Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_request_by_path, error-handling, negative, requests, postman]
requirements: []
---
# ELITEA-1606: PST09 - Get Request by Path (Invalid Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_request_by_path tool properly handles requests for non-existent or invalid request paths, returning a descriptive error.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
NEGATIVE test — request path used does not exist in the collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Invalid request path: NonExistentFolder/FakeRequest

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_request_by_path with POSTMAN_COLLECTION_ID and an invalid path (e.g., NonExistentFolder/FakeRequest) | Tool attempts execution with the invalid path |
| 3 | Capture the tool response | Error returned indicating request not found at path |
| 4 | Validate LLM confirms error returned without exception | LLM confirms descriptive error returned |

## Expected Final State

LLM confirms descriptive error returned

## Pass/Fail Criteria

get_request_by_path returns error for invalid path
Error message indicates request not found
Tool exits cleanly
