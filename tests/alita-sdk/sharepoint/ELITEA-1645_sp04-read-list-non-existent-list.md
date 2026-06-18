---
id: ELITEA-1645
title: "SP04 - Read List (Non-Existent List)"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [error-handling, sharepoint, read_list, negative, lists]
requirements: []
---
# ELITEA-1645: SP04 - Read List (Non-Existent List)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Validates that read_list returns a clear, actionable error when called with a non-existent list name, with no system crashes or unhandled exceptions.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
Confirmed that no list named "NonExistentList_12345_DoesNotExist" exists on the site

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
List title: NonExistentList_12345_DoesNotExist
Limit: 10

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke read_list with list_title=NonExistentList_12345_DoesNotExist and limit=10 | Tool attempts to read the non-existent list |
| 3 | Capture the tool response | Response contains an error message indicating list not found |
| 4 | Validate LLM confirms error is clear, actionable, and no crash occurred | LLM confirms informative error returned without system exception |

## Expected Final State

LLM confirms informative error returned without system exception

## Pass/Fail Criteria

Tool returns an error response (not empty/null)
Error message indicates list not found
Error is clear and actionable
No unhandled exception raised
