---
id: ELITEA-1642
title: "SP10 - Get Files List (Folder Filtering)"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [get_files_list, folder-filter, sharepoint, files]
requirements: []
---
# ELITEA-1642: SP10 - Get Files List (Folder Filtering)

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Validates that get_files_list correctly filters files by folder path, returning only files from the specified folder and handling empty folders gracefully.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
TEST_FOLDER env var is set to an existing folder path in Shared Documents
Valid credentials with read access

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
TEST_FOLDER: relative folder path within Shared Documents (e.g. TestFolder)
Limit: 20

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_files_list with folder_name=TEST_FOLDER and limit_files=20 | Tool accepts folder path parameter |
| 3 | Capture the tool response | Response contains files from the specified folder only, or empty array if folder is empty |
| 4 | Validate LLM confirms folder filtering applied and no error indicators present | LLM confirms correct folder-filtered results returned |

## Expected Final State

LLM confirms correct folder-filtered results returned

## Pass/Fail Criteria

get_files_list returns files from the specified folder only
Empty folder returns empty array, not an error
No error indicators (error, failed, exception, permission denied) in response
No unhandled exception raised
