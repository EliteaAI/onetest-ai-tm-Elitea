---
id: ELITEA-1593
title: "PST22 - Update Collection Variables (Happy Path)"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_variables, collections, postman, smoke]
requirements: []
---
# ELITEA-1593: PST22 - Update Collection Variables (Happy Path)

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates that the update_collection_variables tool successfully updates collection-level variables.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection with write access
Variables: {baseUrl: https://api.example.com, apiVersion: v2}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_collection_variables with POSTMAN_COLLECTION_ID and a dict of variable key-value pairs | Tool accepts parameters and applies the variable update |
| 3 | Capture the tool response and verify success | Tool confirms variables updated without error |
| 4 | Validate LLM confirms variables were updated successfully | LLM confirms collection variables updated |

## Expected Final State

LLM confirms collection variables updated

## Pass/Fail Criteria

update_collection_variables sets provided variables in the collection
Retrieval confirms updated variable values
No exception raised
