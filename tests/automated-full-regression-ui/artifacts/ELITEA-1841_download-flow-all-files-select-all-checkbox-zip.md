---
id: ELITEA-1841
title: "Download Flow – Download All Files Using Select All Checkbox as ZIP"
priority: high
type: functional
module: artifacts
status: ready
execution_type: automated
automation_test_id: tests.ui.artifacts.test_artifacts_download_all_files_select_all_zip.TestArtifactDownloadAllFilesSelectAllZip.test_download_all_files_via_select_all_as_zip
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/676
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1841: Download Flow – Download All Files Using Select All Checkbox as ZIP

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting all files using the header "Select all" checkbox and downloading them produces a ZIP containing all files, with correct progress indicators and a complete file count.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" with subfolder "a1" exists and contains exactly 6 files: "Q&A.docx.odt", "Regression test cases.odt", "sharepoint.docx", "sample_640x426.gif", "sample.png", "sample.txt".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| Total files | 6 |
| File list | Q&A.docx.odt, Regression test cases.odt, sharepoint.docx, sample_640x426.gif, sample.png, sample.txt |
| ZIP file name | bucket-1.zip |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" and navigate to subfolder "a1" | Subfolder "a1" is selected |
| 3 | Verify the file table displays 6 files | All 6 files are listed |
| 4 | Click the "Select all" checkbox in the table header row | All 6 file rows become checked |
| 5 | Verify all 6 file rows become checked | All rows are checked |
| 6 | Verify the header checkbox shows a filled/checked state (not indeterminate) | Header checkbox is fully checked |
| 7 | Verify the "Download files" icon in the top-right is active/enabled with tooltip "Download files" | Download icon is enabled with correct tooltip |
| 8 | Click the "Download files" icon | ZIP preparation modal appears |
| 9 | Verify the "Preparing bucket-1.zip" modal appears with title, progress bar, file counter starting at "1 of 6 files", current file label, and Cancel button | Modal shows all required elements |
| 10 | Verify the counter progresses through all 6 files (e.g. "2 of 6", "3 of 6" ... "6 of 6") | Counter updates through all 6 files |
| 11 | Verify upon completion the modal closes and a ZIP file named "bucket-1.zip" is downloaded | ZIP is downloaded and modal closes |
| 12 | Verify the ZIP file contains all 6 files | All 6 files are in the ZIP |
| 13 | Verify all files are accessible and not corrupted inside the ZIP | Files can be opened from the ZIP |

---

## Expected Final State

All 6 files are downloaded as "bucket-1.zip". Progress modal correctly counts through all files. ZIP is complete and not corrupted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- ZIP contains all 6 files, all accessible; progress counter reaches "6 of 6".

**Fail:**
- Any step produces an error or unexpected result.
- ZIP is missing files, files are corrupted, or progress counter is incorrect.
