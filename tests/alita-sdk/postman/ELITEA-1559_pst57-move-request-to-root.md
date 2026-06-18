---
id: ELITEA-1559
title: "PST57 - Move Request to Root"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [move_request, edge-case, requests, postman]
requirements: []
---
# ELITEA-1559: PST57 - Move Request to Root

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the move_request tool can move a request to the root level of the collection (not inside any folder).

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Request resides in a nested folder
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing request inside a folder
Target folder: (root / empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke move_request with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, and empty/null target folder to indicate root | Tool accepts root target parameter |
| 3 | Capture the tool response and verify request moved to root | Tool confirms request moved to collection root |
| 4 | Validate LLM confirms request is now at collection root | LLM confirms move to root succeeded |

## Expected Final State

LLM confirms move to root succeeded

## Pass/Fail Criteria

move_request to root moves request out of all folders to collection root
Request appears at collection root after move
No exception raised
