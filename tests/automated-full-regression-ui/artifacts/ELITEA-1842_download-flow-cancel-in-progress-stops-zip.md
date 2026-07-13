---
id: ELITEA-1842
title: "Download Flow – Cancel Download in Progress Stops ZIP Preparation"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1842: Download Flow – Cancel Download in Progress Stops ZIP Preparation

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the "Cancel" button during an in-progress ZIP download stops the download immediately, displays a cancellation notification, and leaves the file table and selections unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" with subfolder "a1" contains at least 4 large files suitable for cancellation testing.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| Files to select | Q&A.docx.odt, Regression test cases.odt, sharepoint.docx, sample_640x426.gif (3 or more) |
| Cancellation notification | Download cancelled |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" and navigate to subfolder "a1" | Subfolder "a1" is selected |
| 3 | Select 3 or more files using their checkboxes | Selected files are checked |
| 4 | Click the "Download files" icon in the top-right of the main panel | ZIP preparation progress modal opens |
| 5 | Verify the "Preparing bucket-1.zip" progress modal opens and the download begins | Modal is visible and progress starts |
| 6 | While the download is in progress (e.g. at "1 of 4 files") click the "Cancel" button in the progress modal | Cancel button is clicked mid-download |
| 7 | Verify the progress modal closes immediately | Modal closes |
| 8 | Verify a notification is displayed: "Download cancelled" | "Download cancelled" notification appears |
| 9 | Verify no ZIP file is saved to the local machine (download is aborted) | No ZIP file is in the download directory |
| 10 | Verify the file table remains intact with all files listed and their checkboxes in their previous selected state | File table and checkbox states are unchanged |
| 11 | Verify the selected files remain checked after cancellation | Previously selected files are still checked |

---

## Expected Final State

The ZIP preparation is aborted, the modal closes, and a "Download cancelled" notification appears. No ZIP file is saved. File table and selection states are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Download stops; "Download cancelled" notification shown; no ZIP saved; table unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- ZIP file is saved after Cancel, or file table state is affected by cancellation.
