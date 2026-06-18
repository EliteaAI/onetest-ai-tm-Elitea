---
id: ELITEA-1415
title: "ART19 - SharePoint upload_file: Replace Existing File"
priority: high
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1415: ART19 - SharePoint upload_file: Replace Existing File

**Module:** Artifact · **Priority:** High · **Type:** Functional

**Objective:** Verify the SharePoint upload_file tool replaces an existing file when replace=True, by performing two consecutive uploads of the same artifact file to the same location.

Preconditions:
- SharePoint toolkit is configured with valid credentials
- Artifact toolkit is configured with valid credentials
- SHAREPOINT_TEST_FOLDER exists
- SHAREPOINT_TEST_ARTIFACT_ID points to a valid artifact file

## Preconditions

SharePoint toolkit is configured with SHAREPOINT_TOOLKIT_ID and SHAREPOINT_TOOLKIT_NAME.
Artifact toolkit is configured.
SHAREPOINT_TEST_FOLDER exists.
SHAREPOINT_TEST_ARTIFACT_ID is set to a valid artifact file ID.

## Test Data

folder_path: SHAREPOINT_TEST_FOLDER (env var)
filepath: SHAREPOINT_TEST_ARTIFACT_ID (env var)
filename: 'ART17_test_replace.txt'
replace: true
Both uploads use identical parameters

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure SharePoint and Artifact toolkits | Both toolkits initialized successfully |
| 2 | Call `upload_file` (first time) with folder_path=SHAREPOINT_TEST_FOLDER, filepath=SHAREPOINT_TEST_ARTIFACT_ID, filename='ART17_test_replace.txt', replace=true | First upload completes and returns file metadata with id, webUrl, path |
| 3 | Call `upload_file` again (second time) with identical parameters — same filename and replace=true | Second upload completes without error, replacing the existing file |
| 4 | Verify both results contain valid metadata and the file paths are identical between the two uploads | Both results have id, webUrl, path; paths match each other |
| 5 | LLM validator checks: first_upload_succeeded=true, second_upload_succeeded=true, no errors in either, paths_identical=true | test_results: {test_passed: true, first_upload_succeeded: true, second_upload_succeeded: true, paths_identical: true, no_errors: true} |

## Expected Final State

test_results: {test_passed: true, first_upload_succeeded: true, second_upload_succeeded: true, paths_identical: true, no_errors: true}

## Pass/Fail Criteria

test_passed = true
first_upload_succeeded = true
second_upload_succeeded = true
both_have_metadata = true
paths_identical = true
no_errors = true
