---
id: ELITEA-1864
title: "File Preview/Edit – Unsupported File Type (.zip) Has No Preview and Only Download/Delete in Actions"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_file_preview_unsupported_zip_row_actions.TestArtifactFilePreviewUnsupportedZipRowActions.test_unsupported_zip_row_has_no_preview_and_two_actions
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1696
requirements: []
---

# ELITEA-1864: File Preview/Edit – Unsupported File Type (.zip) Has No Preview and Only Download/Delete in Actions

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that a .zip file does not show the "View/Edit file" icon on hover and that its actions dropdown contains only "Download" and "Delete" options.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "new-file-storage.zip" (ZIP Archive, 230.0 KB).

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | new-file-storage.zip |
| File type | ZIP Archive |
| File size | 230.0 KB |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and click on "bucket-1" | Bucket is selected |
| 2 | Verify "new-file-storage.zip" (ZIP Archive, 230.0 KB) is listed in the file table | File is visible |
| 3 | Hover over the "new-file-storage.zip" file row | Only 3-dot actions icon appears; no View/Edit icon |
| 4 | Verify the "View/Edit file" (loop/magnifier) icon is NOT present on the row for this file type | View/Edit icon is absent |
| 5 | Verify only the 3-dot (ellipsis) actions icon is available on hover | Only actions icon is visible |
| 6 | Click the 3-dot actions icon | Dropdown menu appears |
| 7 | Verify the dropdown contains only "Download" and "Delete" — no preview or view/edit option | Only Download and Delete are present |
| 8 | Click "Download" — verify the ZIP file starts downloading to the local machine | ZIP file download initiates |

---

## Expected Final State

The .zip file has no "View/Edit file" icon on hover. Its actions dropdown contains only "Download" and "Delete". The file downloads successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No View/Edit icon for .zip; actions limited to Download and Delete; download works.

**Fail:**
- Any step produces an error or unexpected result.
- View/Edit icon appears for .zip, or actions menu contains unexpected options.
