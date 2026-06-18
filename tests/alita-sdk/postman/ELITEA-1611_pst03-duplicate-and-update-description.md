---
id: ELITEA-1611
title: "PST03 - Duplicate and Update Description"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_description, duplicate_collection, collections, postman]
requirements: []
---
# ELITEA-1611: PST03 - Duplicate and Update Description

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates duplicate_collection and update_collection_description tools. Tests collection duplication followed by description update and verification.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
New description: Automated test description update

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_collection with POSTMAN_COLLECTION_ID and a unique copy name | New collection ID returned |
| 3 | Invoke update_collection_description on the duplicate with a new description text | Tool confirms description updated |
| 4 | Invoke get_collection on the duplicate and verify description matches | Returned collection description matches the updated text |
| 5 | Invoke delete_collection to clean up the duplicate | Duplicate deleted successfully |
| 6 | Validate LLM confirms all steps succeeded | LLM confirms description was updated and verified |

## Expected Final State

LLM confirms description was updated and verified

## Pass/Fail Criteria

duplicate_collection creates a copy with new ID
update_collection_description applies updated text
get_collection confirms description matches
delete_collection removes copy without error
