---
id: ELITEA-1565
title: "PST54 - Duplicate Request (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [duplicate_request, requests, postman, smoke]
requirements: []
---
# ELITEA-1565: PST54 - Duplicate Request (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the duplicate_request tool successfully creates a copy of an existing request with a new name.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
New name: Duplicated Auto Request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_request with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a new name for the copy | Tool accepts duplication parameters |
| 3 | Capture the tool response and extract new request ID | Response contains new request ID |
| 4 | Delete the duplicated request to clean up | Cleanup successful |
| 5 | Validate LLM confirms duplicate request created | LLM confirms request duplicated with new ID |

## Expected Final State

LLM confirms request duplicated with new ID

## Pass/Fail Criteria

duplicate_request creates a copy of the request with a new unique ID
Duplicated request appears in the same folder
Original request unchanged
No exception raised
