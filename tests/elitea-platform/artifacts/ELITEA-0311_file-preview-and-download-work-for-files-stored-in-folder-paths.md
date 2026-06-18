---
id: ELITEA-0311
title: "File Preview and Download Work for Files Stored in Folder Paths"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [folder-path, regression, artifacts, download, preview, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0311: File Preview and Download Work for Files Stored in Folder Paths

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Preview and Download actions correctly resolve and operate on files whose object keys include a folder prefix.

**Coverage:**
- Preview action opens a file stored under a single-level folder path
- Preview action opens a file stored under a multi-level folder path
- Download action retrieves files stored under folder paths without corruption

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- A text file uploaded to a single-level folder path: test/data.txt
- A text file uploaded to a multi-level folder path: test/folder1/report.txt

## Test Data

- URL: {{base_url}}
- Single-level file: test/data.txt
- Multi-level file: test/folder1/report.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select the bucket. Navigate into folder 'test'. | Folder contents are displayed including data.txt. |
| 2 | Click Preview on data.txt (stored at test/data.txt). | Preview opens and displays file content correctly. No 404 or permission error. |
| 3 | Select data.txt and click Download. | File downloads successfully. File content is intact. |
| 4 | Navigate into test/folder1. Click Preview on report.txt. | Preview opens correctly for the nested file. |
| 5 | Select report.txt and click Download. | File downloads successfully from the multi-level nested path. |

## Expected Final State

File downloads successfully from the multi-level nested path.

## Pass/Fail Criteria

**Pass:**
- Preview works correctly for files at single-level and multi-level folder paths
- Download works correctly for files at single-level and multi-level folder paths
- No 404, 403, or broken URL errors occur

**Fail:**
- Preview fails with an error for any folder-path file
- Download fails or produces a corrupted file
- File operations reference an incorrect object key
