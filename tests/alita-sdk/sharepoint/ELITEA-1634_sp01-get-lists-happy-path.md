---
id: ELITEA-1634
title: "SP01 - Get Lists (Happy Path)"
priority: critical
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [sharepoint, get_lists, lists, smoke]
requirements: []
---
# ELITEA-1634: SP01 - Get Lists (Happy Path)

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Validates that the get_lists tool retrieves all available SharePoint lists from the site, excluding system/hidden lists, with required metadata fields present.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
Valid credentials with read access to the SharePoint site

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
Expected metadata fields: Title, Id, Description, ItemCount, BaseTemplate

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke the get_lists tool with no parameters | Tool accepts the call and begins fetching lists |
| 3 | Capture the tool response | Response contains an array of list objects with Title, Id, Description, ItemCount, and BaseTemplate fields |
| 4 | Validate LLM confirms no error indicators and all required fields are present | LLM confirms successful retrieval without errors |

## Expected Final State

LLM confirms successful retrieval without errors

## Pass/Fail Criteria

get_lists returns at least one list object
Each list has Title, Id, Description, ItemCount, BaseTemplate fields
No error indicators (error, failed, exception, permission denied) in response
No unhandled exception raised
