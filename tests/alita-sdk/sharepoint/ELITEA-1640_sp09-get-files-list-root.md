---
id: ELITEA-1640
title: "SP09 - Get Files List (Root)"
priority: critical
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [get_files_list, sharepoint, smoke, files]
requirements: []
---
# ELITEA-1640: SP09 - Get Files List (Root)

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Validates that get_files_list lists files in the root of the Shared Documents library, returning file objects with Name, Path, Created, Modified, and Link fields.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
Shared Documents library exists on the SharePoint site
Valid credentials with read access

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
Folder name: (empty string — root)
Limit: 50
Expected file fields: Name, Path, Created, Modified, Link

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_files_list with folder_name='' (root) and limit_files=50 | Tool accepts parameters and lists root files |
| 3 | Capture the tool response | Response contains array of file objects (or empty array for empty library) |
| 4 | Validate LLM confirms each file has Name, Path, Created, Modified, Link fields and no error indicators | LLM confirms successful file listing with correct fields |

## Expected Final State

LLM confirms successful file listing with correct fields

## Pass/Fail Criteria

get_files_list returns at least one file or empty array (not error)
Each file object has Name, Path, Created, Modified, and Link fields
Limit of 50 is respected
No error indicators in response
No unhandled exception raised
