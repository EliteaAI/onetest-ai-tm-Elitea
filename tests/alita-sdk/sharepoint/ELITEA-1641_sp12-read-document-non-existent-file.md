---
id: ELITEA-1641
title: "SP12 - Read Document (Non-Existent File)"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [error-handling, read_document, sharepoint, negative, files]
requirements: []
---
# ELITEA-1641: SP12 - Read Document (Non-Existent File)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Validates that read_document returns a clear error including the file path when called with a non-existent file path, without system crashes or unhandled exceptions.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
Confirmed that /sites/YourSite/Shared Documents/NonExistent_File_12345.txt does not exist
Valid credentials with read access

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
File path: /sites/YourSite/Shared Documents/NonExistent_File_12345.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke read_document with path=/sites/YourSite/Shared Documents/NonExistent_File_12345.txt | Tool attempts to read the non-existent file |
| 3 | Capture the tool response | Response contains an error indicating file not found, mentioning the path |
| 4 | Validate LLM confirms error is clear, includes the path, and no crash occurred | LLM confirms informative error returned without system exception |

## Expected Final State

LLM confirms informative error returned without system exception

## Pass/Fail Criteria

Tool returns an error response (not null/empty)
Error message indicates file not found
Error message includes the provided file path
No unhandled exception raised
