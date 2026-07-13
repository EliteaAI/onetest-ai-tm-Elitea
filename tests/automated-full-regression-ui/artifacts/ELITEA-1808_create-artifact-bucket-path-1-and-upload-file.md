---
id: ELITEA-1808
title: "Create Artifact Bucket via \"+ Artifact Bucket\" Button (Path 1) and Upload File"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1808: Create Artifact Bucket via "+ Artifact Bucket" Button (Path 1) and Upload File

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify the primary bucket creation flow using the "+ Artifact Bucket" button, then upload a file to the newly created bucket using the 3-dot menu "Upload files" option, and confirm the file appears in both the main panel and the left panel tree.

---

## Preconditions

- User is logged in to the Elitea platform.
- A test file named "test.txt" is available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Retention policy | Years, 1 (default) |
| Upload file | test.txt |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click the "+ Artifact Bucket" button in the top-left area of the sidebar | "New Bucket" form opens with Name field and Retention policy section |
| 3 | Verify the "New Bucket" form opens with Name field and Retention policy section | Form is visible with all required fields |
| 4 | Enter bucket name: "bucket-1" | Name field accepts and displays "bucket-1" |
| 5 | Leave Retention policy as default (Years, 1) | Retention policy remains at default |
| 6 | Click "Save" | Save operation completes successfully |
| 7 | Verify bucket "bucket-1" appears in the bucket list | "bucket-1" is listed in the left panel bucket list |
| 8 | Click on the 3-dot ellipsis menu next to "bucket-1" | Dropdown menu appears |
| 9 | Select "Upload files" from the dropdown menu | System file explorer window opens |
| 10 | Verify the file explorer window opens | File explorer is open |
| 11 | Select file "test.txt" from the file explorer | "test.txt" is selected |
| 12 | Click "Open" (or "OK") | File is confirmed and "Upload files to ..." modal opens |
| 13 | Verify the "Upload files to ..." modal dialog opens with the Path field showing "bucket-1/" (or default path) | Modal is open with correct path pre-filled |
| 14 | Click the "Upload" button in the modal | Upload operation completes |
| 15 | Verify the file upload completes successfully | Upload success notification or confirmation is displayed |
| 16 | Verify file "test.txt" appears in the right-side files section (main content area) with correct file type, size, and timestamp | "test.txt" is listed in the file table with all metadata populated |
| 17 | Verify file "test.txt" is also listed in the bucket list under "bucket-1" in the left sidebar | "test.txt" appears in the left panel tree under "bucket-1" |

---

## Expected Final State

Bucket "bucket-1" is created and visible in the bucket list. File "test.txt" is uploaded and listed in both the main content area (with correct metadata) and in the left panel tree under "bucket-1".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Bucket is created, file is uploaded and visible in both panels with correct metadata.

**Fail:**
- Any step produces an error or unexpected result.
- Bucket is not created, or file does not appear in the main panel or the left panel tree.
