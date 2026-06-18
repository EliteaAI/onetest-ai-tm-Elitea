---
id: ELITEA-1575
title: "PST41 - Update Request URL with Params"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_url, query-params, requests, postman]
requirements: []
---
# ELITEA-1575: PST41 - Update Request URL with Params

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_url tool properly handles URLs with query parameters and complex URL structures.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
New URL with params: https://httpbin.org/get?param1=value1&amp;param2=value2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_url with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, URL with query parameters included | Tool accepts URL with query params |
| 3 | Capture the tool response and verify URL with params updated | Tool confirms URL and query parameters preserved |
| 4 | Validate LLM confirms URL with query params applied correctly | LLM confirms query parameters preserved in URL update |

## Expected Final State

LLM confirms query parameters preserved in URL update

## Pass/Fail Criteria

update_request_url with query params sets URL and params correctly
URL and params confirmed in collection
No exception raised
