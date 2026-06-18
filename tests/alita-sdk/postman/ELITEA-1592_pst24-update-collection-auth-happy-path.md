---
id: ELITEA-1592
title: "PST24 - Update Collection Auth (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_auth, collections, postman, smoke]
requirements: []
---
# ELITEA-1592: PST24 - Update Collection Auth (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_collection_auth tool successfully updates collection-level authentication settings.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with write access
Auth type: bearer
Token: test-bearer-token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_collection_auth with POSTMAN_COLLECTION_ID, auth_type=bearer, and token value | Tool accepts parameters and applies bearer auth |
| 3 | Capture the tool response and verify success | Tool confirms auth updated without error |
| 4 | Validate LLM confirms collection auth was updated to bearer type | LLM confirms auth update applied |

## Expected Final State

LLM confirms auth update applied

## Pass/Fail Criteria

update_collection_auth sets the specified auth on the collection
Retrieval confirms correct auth type applied
No exception raised
