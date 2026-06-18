---
id: ELITEA-1638
title: "SP02 - Get Lists (Metadata Validation)"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [sharepoint, get_lists, metadata, lists]
requirements: []
---
# ELITEA-1638: SP02 - Get Lists (Metadata Validation)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Validates that each list returned by get_lists has valid metadata: non-empty Title, unique GUID Id, string Description, non-negative ItemCount, and BaseTemplate field.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
Valid credentials with read access to the SharePoint site

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke the get_lists tool with no parameters | Tool returns array of list objects |
| 3 | Capture the tool response and inspect each list object | Each list has a non-empty Title, unique GUID Id, string Description, non-negative ItemCount, and BaseTemplate |
| 4 | Validate LLM confirms all metadata fields meet data type and format requirements | LLM confirms metadata quality is valid across all returned lists |

## Expected Final State

LLM confirms metadata quality is valid across all returned lists

## Pass/Fail Criteria

Every list has a non-empty Title field
Every list has a unique GUID-format Id field
Description field exists on every list (empty string is acceptable)
ItemCount is a non-negative integer
BaseTemplate field is present on every list
