---
id: ELITEA-1599
title: "PST23 - Update Collection Variables (Clear)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_variables, collections, edge-case, postman]
requirements: []
---
# ELITEA-1599: PST23 - Update Collection Variables (Clear)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_collection_variables tool properly handles clearing all collection variables by passing null or empty array.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Collection has pre-existing variables
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with variables
Variables: {} (empty dict)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_collection_variables with POSTMAN_COLLECTION_ID and an empty dict | Tool accepts empty dict and begins update |
| 3 | Capture the tool response | Tool confirms variables cleared or returns empty variable state |
| 4 | Validate LLM confirms all collection variables were cleared | LLM confirms variables cleared successfully |

## Expected Final State

LLM confirms variables cleared successfully

## Pass/Fail Criteria

update_collection_variables with empty dict clears all existing variables
Collection variables are empty after operation
No exception raised
