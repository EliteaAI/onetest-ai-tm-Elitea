---
id: ELITEA-1588
title: "PST27 - Duplicate Collection (Special Characters)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [duplicate_collection, special-chars, collections, edge-case, postman]
requirements: []
---
# ELITEA-1588: PST27 - Duplicate Collection (Special Characters)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the duplicate_collection tool properly handles collection names containing special characters and Unicode.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the workspace

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
New collection name: Test Copy #1 (auto) &amp; backup

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_collection with POSTMAN_COLLECTION_ID and a name containing special characters | Tool accepts name with special characters |
| 3 | Capture the tool response and verify new collection created | Response contains new collection with the special character name |
| 4 | Delete the duplicated collection to clean up | Cleanup successful |
| 5 | Validate LLM confirms special character name preserved in duplicate | LLM confirms collection name with special chars created correctly |

## Expected Final State

LLM confirms collection name with special chars created correctly

## Pass/Fail Criteria

duplicate_collection with special characters in name succeeds
New collection name preserved exactly including special characters
No exception raised
