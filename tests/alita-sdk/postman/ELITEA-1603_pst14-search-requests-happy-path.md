---
id: ELITEA-1603
title: "PST14 - Search Requests (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [search_requests, postman, search, smoke]
requirements: []
---
# ELITEA-1603: PST14 - Search Requests (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the search_requests tool successfully searches for requests across the collection by name.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection contains at least one request matching the search query

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
Search query: partial name of a known request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke search_requests with POSTMAN_COLLECTION_ID and a search query matching known request names | Tool accepts parameters and begins execution |
| 3 | Capture the tool response | Response contains list of matching requests with name and path |
| 4 | Validate LLM confirms at least one result returned matching the search term | LLM confirms search results returned with correct names |

## Expected Final State

LLM confirms search results returned with correct names

## Pass/Fail Criteria

search_requests returns matching requests by name
Each result includes request name and path
No exception raised
