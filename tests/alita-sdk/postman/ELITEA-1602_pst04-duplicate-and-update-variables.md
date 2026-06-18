---
id: ELITEA-1602
title: "PST04 - Duplicate and Update Variables"
priority: high
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_collection_variables, duplicate_collection, collections, postman]
requirements: []
---
# ELITEA-1602: PST04 - Duplicate and Update Variables

**Module:** Postman · **Priority:** High · **Type:** Functional

**Objective:** Validates duplicate_collection and update_collection_variables tools. Tests collection duplication followed by variable updates and verification.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME and POSTMAN_COLLECTION_ID env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
New variable: {key: baseUrl, value: https://api.test.com}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke duplicate_collection with POSTMAN_COLLECTION_ID and a unique copy name | New collection ID returned |
| 3 | Invoke update_collection_variables on the duplicate with new key-value pairs (e.g., [{key: baseUrl, value: https://api.test.com}]) | Tool confirms variables updated |
| 4 | Invoke get_collection on the duplicate and verify variables are present | Returned collection includes the updated variables |
| 5 | Invoke delete_collection to clean up the duplicate | Duplicate deleted successfully |
| 6 | Validate LLM confirms variables were set and verified correctly | LLM confirms all steps completed without error |

## Expected Final State

LLM confirms all steps completed without error

## Pass/Fail Criteria

duplicate_collection creates a copy
update_collection_variables applies new variables
get_collection confirms variables match
delete_collection removes copy without error
