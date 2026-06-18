---
id: ELITEA-1595
title: "PST20 - Update Collection Description (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_description, collections, postman, smoke]
requirements: []
---
# ELITEA-1595: PST20 - Update Collection Description (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_collection_description tool successfully updates the description of a Postman collection.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with write access
New description: Updated by automated test on 2026-02-24

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_collection_description with POSTMAN_COLLECTION_ID and a new description string | Tool accepts parameters and applies the update |
| 3 | Capture the tool response and verify success | Tool confirms description updated without error |
| 4 | Validate LLM confirms description was updated successfully | LLM confirms update applied |

## Expected Final State

LLM confirms update applied

## Pass/Fail Criteria

update_collection_description applies new description
get_collection confirms description matches updated text
No exception raised
