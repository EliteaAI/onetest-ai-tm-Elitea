---
id: ELITEA-1614
title: "PST05 - Get Collection (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [get_collection, collections, postman, smoke]
requirements: []
---
# ELITEA-1614: PST05 - Get Collection (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the get_collection tool successfully retrieves a specific collection in flattened format with path-based structure.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection has at least one folder or request

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with folders and requests

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke get_collection with POSTMAN_COLLECTION_ID | Tool accepts the collection ID and begins execution |
| 3 | Capture the tool response | Response contains the collection structure in flattened path-based format |
| 4 | Validate LLM confirms the collection returned with folder and request paths | LLM confirms flattened structure returned correctly |

## Expected Final State

LLM confirms flattened structure returned correctly

## Pass/Fail Criteria

get_collection returns collection in flattened format
Response includes folders and requests with paths
No exception raised
