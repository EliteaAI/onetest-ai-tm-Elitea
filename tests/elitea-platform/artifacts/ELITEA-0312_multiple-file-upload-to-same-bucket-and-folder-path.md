---
id: ELITEA-0312
title: "Multiple File Upload to Same Bucket and Folder Path"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [folder-path, multi-file, artifacts, upload, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0312: Multiple File Upload to Same Bucket and Folder Path

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when multiple files are selected for upload, all files are uploaded to the same bucket and folder path.

**Coverage:**
- All selected files receive the same folder prefix in their object keys
- No files are skipped, partially uploaded, or placed at a wrong location
- Upload result is consistent for each file in the selection

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Bucket 'excel' exists in Artifacts
- At least 3 test files are available locally: data.xlsx, report.csv, image.png

## Test Data

- URL: {{base_url}}
- Bucket: excel
- Folder path: test/batch
- Files: data.xlsx, report.csv, image.png
- Expected keys: test/batch/data.xlsx, test/batch/report.csv, test/batch/image.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select bucket 'excel'. | Bucket file list is displayed. |
| 2 | Click 'Upload files'. Enter folder path: test/batch. | Upload modal is open with folder path set to 'test/batch'. |
| 3 | Select all three files: data.xlsx, report.csv, image.png. | All three files are listed in the upload selection. |
| 4 | Confirm the upload. | Upload completes. Success indication is shown for all three files. |
| 5 | Navigate into folder 'test', then into 'batch'. Verify all three files are present. | data.xlsx, report.csv, and image.png are all listed under test/batch/. |

## Expected Final State

data.xlsx, report.csv, and image.png are all listed under test/batch/.

## Pass/Fail Criteria

**Pass:**
- All three files are uploaded under test/batch/
- Each file has the correct object key: test/batch/data.xlsx, test/batch/report.csv, test/batch/image.png
- No files are missing or placed at a different path

**Fail:**
- One or more files are uploaded to a different or incorrect path
- Some files are skipped or fail silently
- Files are listed at root instead of inside the folder
