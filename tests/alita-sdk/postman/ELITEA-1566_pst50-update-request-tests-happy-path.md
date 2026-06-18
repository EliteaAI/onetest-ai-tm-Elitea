---
id: ELITEA-1566
title: "PST50 - Update Request Tests (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_tests, scripts, postman, smoke]
requirements: []
---
# ELITEA-1566: PST50 - Update Request Tests (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_tests tool successfully updates the test scripts of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
Test script: pm.test(\"Status is 200\", function () { pm.response.to.have.status(200); });

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_tests with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a JavaScript test script string | Tool accepts test script parameters |
| 3 | Capture the tool response and verify script saved | Tool confirms test script updated without error |
| 4 | Validate LLM confirms test script applied to the request | LLM confirms script saved on request |

## Expected Final State

LLM confirms script saved on request

## Pass/Fail Criteria

update_request_tests sets test script on the request
Script confirmed saved and associated with request
No exception raised
