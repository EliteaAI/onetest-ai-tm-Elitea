---
id: ELITEA-1250
title: "SharePoint index_data Indexes Specified Folder Path Including Nested Subfolders Without Error"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [int:sharepoint, issue:3367, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3367]
---
# ELITEA-1250: SharePoint index_data Indexes Specified Folder Path Including Nested Subfolders Without Error

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that the SharePoint `index_data` tool successfully indexes files from a specified folder path including all nested subfolders, without throwing an `IndexError: list index out of range`.

**Coverage:**
- `index_data` tool execution with an explicit folder path parameter (e.g., `/sites/SiteName/FolderName/`)
- Indexing recurses into nested subfolders within the specified path
- No `IndexError: list index out of range` is thrown for either empty folder configuration or explicit path
- Indexed documents are retrievable after successful indexing

## Preconditions

- Logged in to {{base_url}}
- SharePoint toolkit configured with REST API access and valid credentials
- A SharePoint site exists with at least one folder that contains nested subfolders and files at multiple levels
- The `index_data` tool is available in the configured SharePoint toolkit

## Test Data

- SharePoint site path: /sites/EPAMAlita_test_sam/Alita_test/
- Folder structure: at least 2 levels of nested subfolders, each containing at least 1 file
- Toolkit name: SharePoint toolkit with REST API access
- Tool: index_data

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits. Open the SharePoint toolkit configured with REST API access. | SharePoint toolkit configuration page is displayed with the index_data tool available. |
| 2 | Open the index_data tool. Leave the folder path parameter empty. Execute the tool. | Tool executes without error. Documents from the default site root are indexed successfully. No IndexError is thrown. |
| 3 | Open the index_data tool again. In the folder path parameter, enter a path that contains nested subfolders (e.g., /sites/EPAMAlita_test_sam/Alita_test/). Execute the tool. | Tool executes without error. Indexing starts for the specified folder path. |
| 4 | Wait for the indexing to complete. Observe the result or success message. | Tool completes successfully. Files from the specified folder AND its nested subfolders are indexed. No IndexError: list index out of range is thrown. The indexed document count is non-zero. |
| 5 | Use the search or query capability of the SharePoint toolkit to retrieve a document that was located in a nested subfolder of the indexed path. | The document from the nested subfolder is found and retrievable, confirming that nested folders were indexed correctly. |

## Expected Final State

The document from the nested subfolder is found and retrievable, confirming that nested folders were indexed correctly.

## Pass/Fail Criteria

**Pass:**
- `index_data` completes without errors for both empty folder config and explicit path
- Files from the specified folder and its nested subfolders are indexed
- Indexed document count reflects all files found in the folder tree

**Fail:**
- `IndexError: list index out of range` is thrown during execution
- Only top-level files are indexed and nested subfolders are skipped
- The tool returns an error or no results when a valid path with nested folders is provided
