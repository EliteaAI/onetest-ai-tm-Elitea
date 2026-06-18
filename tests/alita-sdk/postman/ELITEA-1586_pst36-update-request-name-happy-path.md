---
id: ELITEA-1586
title: "PST36 - Update Request Name (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_name, requests, postman, smoke]
requirements: []
---
# ELITEA-1586: PST36 - Update Request Name (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_name tool successfully updates the name of an existing API request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
New name: Renamed Auto Request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_name with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a new name string | Tool accepts rename parameters |
| 3 | Capture the tool response and verify success | Tool confirms request renamed without error |
| 4 | Validate LLM confirms request name updated | LLM confirms rename applied |

## Expected Final State

LLM confirms rename applied

## Pass/Fail Criteria

update_request_name renames the target request
Request appears with new name in collection
No exception raised
