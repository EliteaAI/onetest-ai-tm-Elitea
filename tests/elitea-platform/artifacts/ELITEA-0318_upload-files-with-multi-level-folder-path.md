---
id: ELITEA-0318
title: "Upload Files with Multi-Level Folder Path"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [folder-path, artifacts, nested, upload, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0318: Upload Files with Multi-Level Folder Path

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that files uploaded with a multi-level folder path (e.g., test/folder1) are stored under the full nested prefix and all intermediate folders are implicitly created.

**Coverage:**
- Multi-level path creates the correct nested object key prefix
- All intermediate folders are implicitly created via S3 object key
- File is accessible by navigating the full folder hierarchy in the bucket view

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Bucket 'excel' exists in Artifacts

## Test Data

- URL: {{base_url}}
- Bucket: excel
- Folder path: test/folder1
- Test file: data.xlsx
- Expected object key: test/folder1/data.xlsx

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select bucket 'excel'. | Bucket file list for 'excel' is displayed. |
| 2 | Click 'Upload files'. Enter folder path: test/folder1. | Upload modal opens. Folder path is set to 'test/folder1'. |
| 3 | Select file data.xlsx and confirm the upload. | Upload completes successfully. |
| 4 | Navigate into folder 'test', then into 'folder1'. | Folder hierarchy is navigable. 'test' contains 'folder1'. |
| 5 | Verify data.xlsx is present and its object key is test/folder1/data.xlsx. | File is listed under test/folder1/ with the correct object key. |

## Expected Final State

File is listed under test/folder1/ with the correct object key.

## Pass/Fail Criteria

**Pass:**
- File is uploaded under nested path test/folder1/
- Object key is test/folder1/data.xlsx
- Folder hierarchy is navigable in the bucket view
- No error during upload

**Fail:**
- File lands at root or under a partial path
- Intermediate folders are not created
- Object key is incorrect
- Upload fails
