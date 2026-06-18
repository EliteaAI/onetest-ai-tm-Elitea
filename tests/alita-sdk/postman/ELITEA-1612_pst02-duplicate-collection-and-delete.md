---
id: ELITEA-1612
title: "PST02 - Duplicate Collection and Delete"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [duplicate_collection, delete_collection, collections, lifecycle, postman]
requirements: []
---
# ELITEA-1612: PST02 - Duplicate Collection and Delete

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the duplicate_collection and delete_collection tools work correctly for creating and removing collection copies.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection to duplicate
Duplicate name: Automated Test Copy

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_collection with POSTMAN_COLLECTION_ID and a new unique name | Tool returns the new collection ID of the duplicate |
| 3 | Record the returned duplicate collection ID | Duplicate collection ID captured |
| 4 | Invoke delete_collection with the duplicate collection ID | Tool confirms the collection was deleted |
| 5 | Validate that the LLM confirms duplication and deletion both succeeded | LLM confirms both operations completed without error |

## Expected Final State

LLM confirms both operations completed without error

## Pass/Fail Criteria

duplicate_collection returns new collection ID
delete_collection removes the duplicate without error
No exception raised throughout
