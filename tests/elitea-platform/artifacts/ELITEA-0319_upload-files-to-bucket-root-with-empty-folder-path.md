---
id: ELITEA-0319
title: "Upload Files to Bucket Root with Empty Folder Path"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [regression, artifacts, upload, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0319: Upload Files to Bucket Root with Empty Folder Path

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that files uploaded with an empty folder path are stored directly at the bucket root.

**Coverage:**
- Empty folder path results in a root-level object key (no prefix)
- Files are listed at bucket root after upload
- Backward compatibility with pre-existing upload behavior is preserved

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- At least one S3 bucket exists in Artifacts (e.g., excel)

## Test Data

- URL: {{base_url}}
- Bucket: excel
- Test files: data.xlsx, report.csv
- Expected object keys: data.xlsx, report.csv (no folder prefix)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the sidebar. Select bucket 'excel'. | Bucket file list for 'excel' is displayed. |
| 2 | Click the 'Upload files' button. | Upload modal opens showing the selected bucket name 'excel'. |
| 3 | Leave the folder path field empty. Select files data.xlsx and report.csv. | Files are selected. Folder path field remains empty. |
| 4 | Confirm the upload. | Upload completes successfully. A success indication is shown. |
| 5 | Verify data.xlsx and report.csv appear in the bucket file list at root level with no folder prefix. | Both files are listed directly under the bucket root with no folder grouping. |

## Expected Final State

Both files are listed directly under the bucket root with no folder grouping.

## Pass/Fail Criteria

**Pass:**
- Files upload successfully with no folder path specified
- Object keys are filename only (no prefix): data.xlsx, report.csv
- Files appear at root level in the bucket file list
- Upload completes without errors

**Fail:**
- Files are placed under an unexpected folder prefix
- Upload fails or produces an error
- Files do not appear in the bucket list after upload
