---
id: ELITEA-1635
title: "SP08 - Create List Item (Missing Required Fields)"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [create_list_item, sharepoint, validation, negative, lists]
requirements: []
---
# ELITEA-1635: SP08 - Create List Item (Missing Required Fields)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Validates that create_list_item returns a clear validation error when required fields (e.g. Title) are missing from the item payload, without system crashes.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
TEST_LIST_NAME env var is set to an existing SharePoint list with a required Title field
Valid credentials with write access to the list

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
TEST_LIST_NAME: name of the target SharePoint list
Item fields: {} (empty dict — no fields provided)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke create_list_item with TEST_LIST_NAME and an empty fields dict {} | Tool attempts to create item with no fields |
| 3 | Capture the tool response | Response contains a validation error about missing required fields |
| 4 | Validate LLM confirms error specifies missing field and no crash occurred | LLM confirms clear validation error returned without system exception |

## Expected Final State

LLM confirms clear validation error returned without system exception

## Pass/Fail Criteria

Tool returns an error response (not null/empty)
Error indicates required field is missing
Error specifies which field is missing (typically Title)
No unhandled exception raised
