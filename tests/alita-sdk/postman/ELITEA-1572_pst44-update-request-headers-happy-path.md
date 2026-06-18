---
id: ELITEA-1572
title: "PST44 - Update Request Headers (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_headers, requests, postman, smoke]
requirements: []
---
# ELITEA-1572: PST44 - Update Request Headers (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_headers tool successfully updates the headers of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
Headers: {Content-Type: application/json, X-Custom-Header: test-value}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_headers with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a dict of header key-value pairs | Tool accepts header dict parameters |
| 3 | Capture the tool response and verify success | Tool confirms headers updated without error |
| 4 | Validate LLM confirms headers set on the request | LLM confirms header update applied |

## Expected Final State

LLM confirms header update applied

## Pass/Fail Criteria

update_request_headers sets provided headers on request
Headers confirmed saved in collection
No exception raised
