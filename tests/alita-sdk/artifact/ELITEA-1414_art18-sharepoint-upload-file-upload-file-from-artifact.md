---
id: ELITEA-1414
title: "ART18 - SharePoint upload_file: Upload File from Artifact"
priority: critical
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1414: ART18 - SharePoint upload_file: Upload File from Artifact

**Module:** Artifact · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the SharePoint upload_file tool uploads a file from artifact storage to a document library, returning full file metadata (id, webUrl, path, size, mime_type).

Preconditions:
- SharePoint toolkit is configured with valid credentials
- Artifact toolkit is configured with valid credentials
- SHAREPOINT_TEST_FOLDER exists in the document library
- SHAREPOINT_TEST_ARTIFACT_ID points to a valid artifact file

## Preconditions

SharePoint toolkit is configured with SHAREPOINT_TOOLKIT_ID and SHAREPOINT_TOOLKIT_NAME.
Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
SHAREPOINT_TEST_FOLDER exists in the document library.
SHAREPOINT_TEST_ARTIFACT_ID is set to a valid artifact file ID.

## Test Data

folder_path: SHAREPOINT_TEST_FOLDER (env var)
filepath: SHAREPOINT_TEST_ARTIFACT_ID (env var, artifact file ID)
filename: 'ART16_test_upload.txt'
replace: true

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure SharePoint toolkit with SHAREPOINT_TOOLKIT_ID and SHAREPOINT_TOOLKIT_NAME; configure Artifact toolkit with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME | Both toolkits initialized successfully |
| 2 | Set parameters: folder_path=SHAREPOINT_TEST_FOLDER, filepath=SHAREPOINT_TEST_ARTIFACT_ID, filename='ART16_test_upload.txt', replace=true | Parameters are ready |
| 3 | Call `upload_file` tool with folder_path, filepath (artifact ID), filename, and replace=true | Tool executes without error |
| 4 | Verify the result contains all required metadata fields: id, webUrl, path (containing folder and filename), size (>0), mime_type | All metadata fields are present and valid |
| 5 | LLM validator checks: file_uploaded=true, has_id=true, has_webUrl=true, path contains filename, size is positive, no error messages | test_results: {test_passed: true, file_uploaded: true, has_id: true, has_webUrl: true, has_path: true, has_size: true, has_mime_type: true} |

## Expected Final State

test_results: {test_passed: true, file_uploaded: true, has_id: true, has_webUrl: true, has_path: true, has_size: true, has_mime_type: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
file_uploaded = true
has_id = true
has_webUrl = true
has_path = true
has_size = true
has_mime_type = true
no_errors = true
