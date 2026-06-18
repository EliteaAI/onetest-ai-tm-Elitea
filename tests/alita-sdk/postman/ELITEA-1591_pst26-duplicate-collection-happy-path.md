---
id: ELITEA-1591
title: "PST26 - Duplicate Collection (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [duplicate_collection, collections, postman, smoke]
requirements: []
---
# ELITEA-1591: PST26 - Duplicate Collection (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the duplicate_collection tool successfully creates a copy of an existing collection with a new name.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the workspace

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
New collection name: Automated Test Duplicate

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_collection with POSTMAN_COLLECTION_ID and a new name for the copy | Tool accepts parameters and creates duplicate |
| 3 | Capture the tool response and extract the new collection ID | Response contains new collection ID |
| 4 | Delete the duplicated collection to clean up | Cleanup successful |
| 5 | Validate LLM confirms duplication was successful | LLM confirms duplicate collection created with new ID |

## Expected Final State

LLM confirms duplicate collection created with new ID

## Pass/Fail Criteria

duplicate_collection creates a new collection with unique ID
Duplicated collection contains same requests as source
Original collection unchanged
No exception raised
