---
id: ELITEA-1569
title: "PST48 - Update Request Auth (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_auth, requests, postman, smoke]
requirements: []
---
# ELITEA-1569: PST48 - Update Request Auth (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_request_auth tool successfully updates the authentication settings of an existing request.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request
Auth type: bearer
Token: auto-test-bearer-token

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_auth with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, auth_type=bearer, and token value | Tool accepts bearer auth parameters |
| 3 | Capture the tool response and verify auth updated | Tool confirms auth set to bearer type |
| 4 | Validate LLM confirms bearer auth applied to the request | LLM confirms auth update with bearer token applied |

## Expected Final State

LLM confirms auth update with bearer token applied

## Pass/Fail Criteria

update_request_auth sets bearer token auth on the request
Auth type confirmed as bearer with correct token
No exception raised
