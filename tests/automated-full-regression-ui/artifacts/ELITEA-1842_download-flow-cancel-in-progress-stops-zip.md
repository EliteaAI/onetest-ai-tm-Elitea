---
id: ELITEA-1842
title: "Download Flow – Cancel In-Progress ZIP Preparation via Cancel Button or Close X"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1842: Download Flow – Cancel In-Progress ZIP Preparation via Cancel Button or Close X

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that stopping an in-progress ZIP download — via either the "Cancel" button or the X (close) icon on the progress modal — stops the download immediately, displays a cancellation notification, and leaves the file table and selections unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" with subfolder "a1" contains at least 4 files suitable for cancellation testing.

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

### Part 1: Cancel via "Cancel" Button

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

### Part 2: Cancel via X (Close) Icon

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | With the same or a new selection of 3 or more files, click the "Download files" icon in the top-right of the main panel | ZIP preparation progress modal opens |
| 13 | Verify the "Preparing bucket-1.zip" progress modal opens and the download begins | Modal is visible and progress starts |
| 14 | Click the X (close) icon in the top-right corner of the progress modal | Modal closes |
| 15 | Verify the progress modal closes immediately | Modal is no longer visible |
| 16 | Verify a notification is displayed: "Download cancelled" | "Download cancelled" notification appears |
| 17 | Verify no ZIP file is saved to the local machine | No ZIP file in downloads |

---

## Expected Final State

Both the "Cancel" button and the X (close) icon abort the ZIP preparation, close the modal, and show a "Download cancelled" notification. No ZIP file is saved in either case. File table and selection states are unchanged after Cancel.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both Cancel button and X icon stop the download, show "Download cancelled", and leave no ZIP file saved.
- File table and checkbox state remain intact after Cancel.

**Fail:**
- Any step produces an error or unexpected result.
- ZIP file is saved after either cancellation method, or file table state is affected.

---

## Notes

**Source functional tests:** ELITEA-1842, ELITEA-1843

**Regression rationale:** Both tests assert identical "cancel in-progress ZIP" behavior and differ only in which control dismisses the modal (Cancel button vs X icon); consolidating avoids duplicated multi-file-selection setup.

**Selected checkpoints:**
- Cancel button stops download mid-progress, no ZIP saved, selections preserved (ELITEA-1842)
- X (close) icon stops download, no ZIP saved (ELITEA-1843)
