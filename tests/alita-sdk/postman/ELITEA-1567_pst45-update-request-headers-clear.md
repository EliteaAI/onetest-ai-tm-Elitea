---
id: ELITEA-1567
title: "PST45 - Update Request Headers (Clear)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_headers, edge-case, requests, postman]
requirements: []
---
# ELITEA-1567: PST45 - Update Request Headers (Clear)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_headers tool properly handles clearing all request headers by passing empty array.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Request has existing headers set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to a request with headers
Headers: {} (empty dict)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_headers with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and an empty dict | Tool accepts empty header dict |
| 3 | Capture the tool response | Tool confirms headers cleared without error |
| 4 | Validate LLM confirms all headers removed from the request | LLM confirms headers cleared |

## Expected Final State

LLM confirms headers cleared

## Pass/Fail Criteria

update_request_headers with empty dict clears all headers
Request has no custom headers after operation
No exception raised
