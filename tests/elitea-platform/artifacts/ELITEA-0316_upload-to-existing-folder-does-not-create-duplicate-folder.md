---
id: ELITEA-0316
title: "Upload to Existing Folder Does Not Create Duplicate Folder"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [existing-folder, folder-path, artifacts, upload, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0316: Upload to Existing Folder Does Not Create Duplicate Folder

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that uploading files to a folder path that already exists places the files in the existing folder without creating duplicate folder entries.

**Coverage:**
- Existing folder path is reused correctly on upload
- No duplicate folder entries appear in the bucket view
- Pre-existing files in the folder remain intact after the new upload

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Bucket 'excel' exists with an existing folder 'test' containing at least one file (e.g., test/existing.txt)

## Test Data

- URL: {{base_url}}
- Bucket: excel
- Existing folder: test
- Pre-existing file: test/existing.txt
- New upload file: data.xlsx
- Expected: both existing.txt and data.xlsx present under test/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select bucket 'excel'. Confirm folder 'test' already exists with existing.txt inside. | Folder 'test' is visible in the file list. |
| 2 | Click 'Upload files'. Enter folder path: test. Select file data.xlsx. Confirm the upload. | Upload completes successfully. |
| 3 | Navigate into folder 'test'. | Folder opens and shows its contents. |
| 4 | Verify both existing.txt and data.xlsx are present inside 'test'. | Both files are listed with no data loss. |
| 5 | Navigate back to the bucket root. Count the number of 'test' folder entries. | Only one 'test' folder entry exists at root level. No duplicates. |

## Expected Final State

Only one 'test' folder entry exists at root level. No duplicates.

## Pass/Fail Criteria

**Pass:**
- New file is placed inside the existing folder
- No duplicate folder entries are created
- Pre-existing files in the folder are intact

**Fail:**
- A second 'test' folder entry appears in the bucket list
- Pre-existing files are removed or overwritten unexpectedly
- Upload fails
