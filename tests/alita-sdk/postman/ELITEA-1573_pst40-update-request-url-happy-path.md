---
id: ELITEA-1573
title: "PST40 - Update Request URL (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_url, requests, postman, smoke]
requirements: []
---
# ELITEA-1573: PST40 - Update Request URL (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_url tool successfully updates the URL of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
New URL: https://httpbin.org/anything

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_url with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and a new URL string | Tool accepts URL update parameters |
| 3 | Capture the tool response and verify URL updated | Tool confirms URL updated without error |
| 4 | Validate LLM confirms URL update applied | LLM confirms new URL set on the request |

## Expected Final State

LLM confirms new URL set on the request

## Pass/Fail Criteria

update_request_url sets new URL on the request
URL confirmed updated in collection
No exception raised
