---
id: ELITEA-1601
title: "PST15 - Search Requests (Method Filter)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [search_requests, filtering, postman, search]
requirements: []
---
# ELITEA-1601: PST15 - Search Requests (Method Filter)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the search_requests tool properly applies HTTP method filters when searching for requests.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains GET requests

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with GET requests
HTTP method filter: GET

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke search_requests with POSTMAN_COLLECTION_ID, no name query, and method filter set to GET | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains only GET requests |
| 4 | Validate LLM confirms all returned requests have method GET | LLM confirms method filter applied correctly |

## Expected Final State

LLM confirms method filter applied correctly

## Pass/Fail Criteria

search_requests with method filter returns only requests matching that HTTP method
All results have the specified method
No exception raised
