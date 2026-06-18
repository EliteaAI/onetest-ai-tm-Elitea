---
id: ELITEA-1637
title: "SP06 - Get List Columns (Invalid List)"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [get_list_columns, error-handling, sharepoint, negative, lists]
requirements: []
---
# ELITEA-1637: SP06 - Get List Columns (Invalid List)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Validates that get_list_columns returns a clear error when called with a non-existent list name, with no crashes or unhandled exceptions.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
Confirmed that no list named "InvalidList_99999_DoesNotExist" exists on the site

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
List title: InvalidList_99999_DoesNotExist

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_list_columns with list_title=InvalidList_99999_DoesNotExist | Tool attempts to fetch columns for the non-existent list |
| 3 | Capture the tool response | Response contains an error message indicating list not found |
| 4 | Validate LLM confirms error is informative and no crash occurred | LLM confirms clear error returned without system exception |

## Expected Final State

LLM confirms clear error returned without system exception

## Pass/Fail Criteria

Tool returns an error response (not empty/null)
Error message indicates list not found
Error is clear and actionable
No unhandled exception raised
