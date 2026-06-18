---
id: ELITEA-1615
title: "PST01 - Get Collections (Happy Path)"
priority: critical
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_collections, collections, postman, smoke]
requirements: []
---
# ELITEA-1615: PST01 - Get Collections (Happy Path)

**Module:** Postman · **Priority:** Critical · **Type:** Functional

**Objective:** Validates that the get_collections tool successfully retrieves all Postman collections accessible to the configured user account.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME env var is set
Postman API key has access to at least one collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
Postman API key must have read access to collections

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME env var and valid API key | Toolkit initializes and connects without error |
| 2 | Invoke the get_collections tool with no filters | Tool accepts the request and begins execution |
| 3 | Capture the tool response | Response contains a list of collections each with id and name fields |
| 4 | Validate that the LLM confirms at least one collection is returned with expected structure | LLM confirms collection list returned successfully |

## Expected Final State

LLM confirms collection list returned successfully

## Pass/Fail Criteria

get_collections returns non-empty list of collections
Each collection has id and name
No exception raised
