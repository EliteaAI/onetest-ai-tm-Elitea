---
id: ELITEA-0281
title: "File upload and deletion remain functional after a bucket is pinned"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, r-2.0.3, 4180]
requirements: [EliteaAI/elitea_issues#4180]
---
# ELITEA-0281: File upload and deletion remain functional after a bucket is pinned

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that pinning a bucket does not break file upload or file deletion operations within that bucket.

**Coverage:**
- File upload completes successfully in a pinned bucket
- Uploaded file appears in the file table with correct metadata
- File deletion works correctly from a pinned bucket
- Bucket remains pinned throughout file operations
- No console errors or error toasts during file operations

## Preconditions

- Logged in to ELITEA ({{base_url}}
- At least one bucket is pinned and accessible
- A test file is available for upload

## Test Data

- Pinned bucket: any available pinned bucket (e.g., `bucket-for-agent1`)
- Upload file: `test-file.txt` (any small plain text file)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the left sidebar. | Artifacts page opens; the pinned bucket is visible at the top with 📌 icon. |
| 2 | Click on the pinned bucket to open its file list. | Bucket file list opens in the main area; breadcrumb shows the bucket name. |
| 3 | Click the 'Upload' button in the file table toolbar. | File selection dialog opens. |
| 4 | Select `test-file.txt` and confirm the upload. | Upload completes; success indicator is shown. |
| 5 | Verify `test-file.txt` appears in the file table. | File entry shows correct name, file type, and size; no error message. |
| 6 | Verify the bucket is still pinned at the top with 📌 icon. | Bucket remains pinned; icon unchanged. |
| 7 | Select `test-file.txt` using the checkbox in the file table. | Checkbox is checked; Delete action becomes active in the toolbar. |
| 8 | Click the Delete icon in the toolbar and confirm the deletion. | `test-file.txt` is removed from the file table; no error toast. |
| 9 | Verify the bucket remains pinned at the top with 📌 icon. | Bucket is still at the top with the filled pin icon. |

## Expected Final State

Bucket is still at the top with the filled pin icon.

## Pass/Fail Criteria

**Pass:**
- Upload and deletion succeed without errors
- Bucket remains pinned throughout all file operations
- No error toasts or console errors at any step

**Fail:**
- Upload fails or file does not appear in the table
- File deletion does not complete
- Bucket becomes unpinned after file operations
- Error toast or console error appears
