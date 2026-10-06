---
id: ELITEA-1824
title: "Upload Files to Bucket Subfolder via Three Upload Options and Verify Bucket Selection and Contents"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1824: Upload Files to Bucket Subfolder via Three Upload Options and Verify Bucket Selection and Contents

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify all three upload paths (center button, top-right upload icon, bucket 3-dot menu) work correctly, that uploaded files appear in their correct subfolder locations, and that the URL reflects the selected bucket and folder path.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists and is empty.
- Test files "sample.txt", "sample.png", and "sample.md" are available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder name | a1 |
| Upload file 1 | sample.txt |
| Upload file 2 | sample.png |
| Upload file 3 | sample.md |
| Path for option 1 & 2 | bucket-1/a1 |
| Path for option 3 | bucket-1 (root) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Verify that bucket "bucket-1" exists in the bucket list | "bucket-1" is visible |
| 3 | Click on "bucket-1" in the bucket list | Main panel shows "No files in this bucket" with "Upload files" button |
| 4 | Verify the main panel shows "No files in this bucket" message with an "Upload files" button in the center | Empty state is displayed |
| 5 | Click the "Upload files" button in the center of the main panel | System file explorer opens |
| 6 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 7 | Navigate to the test data folder and select file "sample.txt" | "sample.txt" is selected |
| 8 | Click "Open" in the file explorer | "Upload files to ..." modal opens |
| 9 | Verify the "Upload files to ..." modal opens with a "Path" field pre-filled with "bucket-1" | Modal is open with path pre-filled |
| 10 | In the Path field append "/a1" so the path reads "bucket-1/a1" | Path field shows "bucket-1/a1" |
| 11 | Click "Upload" button in the modal | Upload completes |
| 12 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 13 | Verify in the left panel "bucket-1" expands and subfolder "a1" appears beneath it | "a1" subfolder is visible under "bucket-1" |
| 14 | Verify the main panel header displays the path "bucket-1 > a1" | Breadcrumb shows "bucket-1 > a1" |
| 15 | Verify "sample.txt" is listed in the file table with Name, Type, Size and Last update populated | "sample.txt" is listed with all metadata |
| 16 | Click the upload icon in the top-right corner of the main panel (tooltip: "Upload files") | System file explorer opens |
| 17 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 18 | Navigate to the test data folder and select file "sample.png" | "sample.png" is selected |
| 19 | Click "Open" in the file explorer | "Upload files to ..." modal opens |
| 20 | Verify the "Upload files to ..." modal opens with a "Path" field pre-filled with "bucket-1/a1" | Modal shows path "bucket-1/a1" |
| 21 | Verify the path remains "bucket-1/a1" (no changes needed) | Path is correct |
| 22 | Click "Upload" button in the modal | Upload completes |
| 23 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 24 | Verify "sample.png" is listed in the file table in the "bucket-1 > a1" view alongside "sample.txt" | Both files are listed |
| 25 | In the left panel hover over "bucket-1" and click the 3-dot (ellipsis) / actions icon next to the bucket name | Dropdown menu appears |
| 26 | Verify a dropdown menu appears with options: "Upload files", "Pin to top", "Edit", "Delete" | All options are visible |
| 27 | Click "Upload files" | System file explorer opens |
| 28 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 29 | Navigate to the test data folder and select file "sample.md" | "sample.md" is selected |
| 30 | Click "Open" in the file explorer | "Upload files to ..." modal opens |
| 31 | Verify the "Upload files to ..." modal opens with a "Path" field pre-filled with "bucket-1" | Modal shows root path "bucket-1" |
| 32 | Verify the path is only "bucket-1" without sub-folder | Path shows "bucket-1" only |
| 33 | Click "Upload" button in the modal | Upload completes |
| 34 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 35 | Verify the main panel header displays the path "bucket-1" (root level, no subfolder) | Breadcrumb shows "bucket-1" |
| 36 | Verify "sample.md" is listed in the file table at the root level of "bucket-1" in folder tree | "sample.md" is at root level |
| 37 | In the left panel click on "bucket-1" | "bucket-1" is selected |
| 38 | Verify "bucket-1" is highlighted (selected state) and expands to show subfolder "a1" beneath it | Bucket is selected and "a1" is visible |
| 39 | Click on subfolder "a1" under "bucket-1" in the left panel | "a1" is selected |
| 40 | Verify "a1" is highlighted and the main panel header displays "bucket-1 > a1" | "a1" is highlighted and breadcrumb is correct |
| 41 | Verify the file table in the main panel contains exactly 2 files: "sample.txt" and "sample.png" | Exactly 2 files are listed |
| 42 | Verify "sample.md" is NOT listed in the "bucket-1 > a1" view | "sample.md" is absent from subfolder view |
| 43 | Click on "bucket-1" in the left panel (root level) | Root level contents are shown |
| 44 | Verify the main panel header displays "bucket-1" | Breadcrumb shows "bucket-1" |
| 45 | Verify "sample.md" is listed in the file table at the root level of "bucket-1" | "sample.md" is at root |
| 46 | Verify the URL in the browser address bar reflects the selected bucket and folder path | URL shows correct bucket and folder parameters |

---

## Expected Final State

All three upload options work correctly. "sample.txt" and "sample.png" are in subfolder "a1"; "sample.md" is at the root of "bucket-1". The URL reflects the selected bucket and folder path correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Files uploaded via all three options appear in correct locations; URL reflects current selection.

**Fail:**
- Any upload option fails, or files appear in incorrect locations, or URL does not update correctly.
