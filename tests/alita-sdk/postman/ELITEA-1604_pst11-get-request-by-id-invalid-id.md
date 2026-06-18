---
id: ELITEA-1604
title: "PST11 - Get Request by ID (Invalid ID)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_request_by_id, error-handling, negative, requests, postman]
requirements: []
---
# ELITEA-1604: PST11 - Get Request by ID (Invalid ID)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_request_by_id tool properly handles requests with non-existent or invalid request IDs, returning a descriptive error.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
NEGATIVE test — request ID used does not exist

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Invalid request ID: fake-request-id-000

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_request_by_id with POSTMAN_COLLECTION_ID and a non-existent request ID (e.g., fake-request-id-000) | Tool attempts execution with the invalid ID |
| 3 | Capture the tool response | Error returned indicating request ID not found |
| 4 | Validate LLM confirms error returned without exception | LLM confirms descriptive error returned |

## Expected Final State

LLM confirms descriptive error returned

## Pass/Fail Criteria

get_request_by_id returns error for invalid ID
Error message indicates request not found
Tool exits cleanly
