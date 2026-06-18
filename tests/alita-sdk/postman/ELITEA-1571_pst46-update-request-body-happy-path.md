---
id: ELITEA-1571
title: "PST46 - Update Request Body (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_body, requests, postman, smoke]
requirements: []
---
# ELITEA-1571: PST46 - Update Request Body (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_body tool successfully updates the body of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing POST request
Body type: raw
Body content: {\"name\": \"test\", \"active\": true}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_body with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, body_type=raw, and JSON content | Tool accepts raw JSON body parameters |
| 3 | Capture the tool response and verify body updated | Tool confirms body set to raw JSON |
| 4 | Validate LLM confirms raw body applied to the request | LLM confirms body update applied with correct mode |

## Expected Final State

LLM confirms body update applied with correct mode

## Pass/Fail Criteria

update_request_body sets raw JSON body on the request
Body mode and content confirmed in collection
No exception raised
