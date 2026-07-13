---
id: ELITEA-1840
title: "Download Flow – Download Multiple Selected Files as ZIP via Download Icon"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1840: Download Flow – Download Multiple Selected Files as ZIP via Download Icon

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that selecting multiple files and clicking the "Download files" icon triggers a ZIP preparation modal with progress indicators, and the resulting ZIP contains exactly the selected files.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" with subfolder "a1" exists and contains at least 4 files including "sample.txt" and "sample.png".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| Files to select | sample.txt, sample.png |
| ZIP file name | bucket-1.zip |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" and navigate to subfolder "a1" | Subfolder "a1" is selected |
| 3 | Verify the file table displays at least 4 files including "sample.txt" and "sample.png" | Files are visible |
| 4 | Click the checkbox next to "sample.txt" — verify it becomes checked | "sample.txt" is checked |
| 5 | Click the checkbox next to "sample.png" — verify it becomes checked | "sample.png" is checked |
| 6 | Verify 2 files are selected and the remaining files remain unchecked | Exactly 2 files are checked |
| 7 | Verify the "Download files" icon in the top-right of the main panel becomes active/enabled | Download icon is enabled |
| 8 | Click the "Download files" icon in the top-right of the main panel | ZIP preparation modal appears |
| 9 | Verify a "Preparing bucket-1.zip" progress modal appears with title, progress bar, file counter, current file label, and "Cancel" button | Modal shows all required elements |
| 10 | Verify the progress counter and current file label update as each file is processed | Counter and label update in real time |
| 11 | Verify the progress bar advances as files are downloaded | Progress bar moves forward |
| 12 | Verify upon completion the modal closes and a ZIP file named "bucket-1.zip" is downloaded to the local machine | ZIP file is downloaded and modal closes |
| 13 | Verify the ZIP file contains exactly 2 files: "sample.txt" and "sample.png" | ZIP contains exactly the 2 selected files |
| 14 | Verify none of the unselected files are included in the ZIP | No unselected files in ZIP |

---

## Expected Final State

A ZIP file named "bucket-1.zip" containing exactly "sample.txt" and "sample.png" is downloaded. The progress modal displays correct indicators and closes on completion.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- ZIP contains exactly the selected files; progress modal shows correct indicators.

**Fail:**
- Any step produces an error or unexpected result.
- ZIP is missing files, contains extra files, or progress modal does not appear.
