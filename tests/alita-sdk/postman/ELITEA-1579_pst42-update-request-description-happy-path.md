---
id: ELITEA-1579
title: "PST42 - Update Request Description (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_description, requests, postman, smoke]
requirements: []
---
# ELITEA-1579: PST42 - Update Request Description (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_description tool successfully updates the description of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
Description: This request was updated by automated test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_description with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and description text | Tool accepts description update parameters |
| 3 | Capture the tool response and verify success | Tool confirms description updated without error |
| 4 | Validate LLM confirms description updated on the request | LLM confirms description change applied |

## Expected Final State

LLM confirms description change applied

## Pass/Fail Criteria

update_request_description sets description text on the request
Description confirmed saved in collection
No exception raised
