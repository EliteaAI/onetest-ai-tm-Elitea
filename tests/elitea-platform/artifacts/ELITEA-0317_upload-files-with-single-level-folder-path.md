---
id: ELITEA-0317
title: "Upload Files with Single-Level Folder Path"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [folder-path, artifacts, upload, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0317: Upload Files with Single-Level Folder Path

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that files uploaded with a single-level folder path are stored under that folder prefix and the folder is implicitly created.

**Coverage:**
- Single folder name creates the correct object key prefix
- Folder is implicitly created on upload via S3 object key
- File is accessible within the folder in the bucket view

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Bucket 'excel' exists in Artifacts

## Test Data

- URL: {{base_url}}
- Bucket: excel
- Folder path: test
- Test file: data.xlsx
- Expected object key: test/data.xlsx

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select bucket 'excel'. | Bucket file list for 'excel' is displayed. |
| 2 | Click 'Upload files'. When the upload modal opens, enter folder path: test. | Upload modal opens. Folder path field is populated with 'test'. |
| 3 | Select file data.xlsx and confirm the upload. | Upload completes successfully. |
| 4 | Verify that a folder entry 'test' appears in the bucket file list. Click into it. | Folder 'test' is listed in the bucket. Navigating into it shows data.xlsx. |
| 5 | Verify the object key of data.xlsx is test/data.xlsx (via UI or API). | Object key matches test/data.xlsx. |

## Expected Final State

Object key matches test/data.xlsx.

## Pass/Fail Criteria

**Pass:**
- Folder 'test' is created implicitly in the bucket
- data.xlsx is accessible under test/
- Object key is test/data.xlsx
- No error during upload

**Fail:**
- File is uploaded to root instead of test/
- Object key does not include the folder prefix
- Folder does not appear in the bucket view
- Upload fails with an error
