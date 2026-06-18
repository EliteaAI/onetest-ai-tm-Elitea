---
id: ELITEA-1561
title: "PST51 - Update Request Tests (Clear)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_tests, edge-case, scripts, postman]
requirements: []
---
# ELITEA-1561: PST51 - Update Request Tests (Clear)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_tests tool properly handles clearing test scripts by setting them to empty string.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Request has an existing test script
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to a request with an existing test script
Script: (empty string)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_tests with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and an empty string | Tool accepts empty script string |
| 3 | Capture the tool response | Tool confirms test script cleared without error |
| 4 | Validate LLM confirms test script removed from the request | LLM confirms script cleared |

## Expected Final State

LLM confirms script cleared

## Pass/Fail Criteria

update_request_tests with empty string clears the test script
Request has no test script after operation
No exception raised
