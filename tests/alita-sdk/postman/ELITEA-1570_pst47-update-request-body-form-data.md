---
id: ELITEA-1570
title: "PST47 - Update Request Body (Form Data)"
priority: medium
type: functional
module: postman
status: ready
execution_type: automated
tags: [update_request_body, form-data, requests, postman]
requirements: []
---
# ELITEA-1570: PST47 - Update Request Body (Form Data)

**Module:** Postman · **Priority:** Medium · **Type:** Functional

**Objective:** Validates that the update_request_body tool properly handles updating request body with form data mode.

## Preconditions

Postman toolkit is configured and authenticated
POSTMAN_TOOLKIT_NAME, POSTMAN_COLLECTION_ID, and POSTMAN_REQUEST_PATH env vars are set
Write access to the target collection

## Test Data

POSTMAN_TOOLKIT_NAME: name of configured Postman toolkit
POSTMAN_COLLECTION_ID: ID of existing collection
POSTMAN_REQUEST_PATH: path to an existing POST request
Body type: formdata
Form fields: [{key: field1, value: val1}, {key: field2, value: val2}]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the Postman toolkit using POSTMAN_TOOLKIT_NAME and valid API key | Toolkit initializes without error |
| 2 | Invoke update_request_body with POSTMAN_COLLECTION_ID, POSTMAN_REQUEST_PATH, body_type=formdata, and form fields | Tool accepts form-data body parameters |
| 3 | Capture the tool response and verify form-data body set | Tool confirms body set to form-data type |
| 4 | Validate LLM confirms form-data body applied correctly | LLM confirms form fields preserved in body update |

## Expected Final State

LLM confirms form fields preserved in body update

## Pass/Fail Criteria

update_request_body with form-data type sets form fields correctly
Body mode confirmed as form-data with expected fields
No exception raised
