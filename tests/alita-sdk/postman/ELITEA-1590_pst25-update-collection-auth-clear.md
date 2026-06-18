---
id: ELITEA-1590
title: "PST25 - Update Collection Auth (Clear)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_auth, collections, edge-case, postman]
requirements: []
---
# ELITEA-1590: PST25 - Update Collection Auth (Clear)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_collection_auth tool properly handles clearing collection authentication by passing null.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection has existing auth configured
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with auth configured
Auth type: noauth

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_collection_auth with POSTMAN_COLLECTION_ID and auth_type=noauth | Tool accepts parameters and removes auth |
| 3 | Capture the tool response | Tool confirms auth cleared without error |
| 4 | Validate LLM confirms collection auth was cleared | LLM confirms auth removed successfully |

## Expected Final State

LLM confirms auth removed successfully

## Pass/Fail Criteria

update_collection_auth with auth_type=noauth clears existing auth
Collection has no auth after operation
No exception raised
