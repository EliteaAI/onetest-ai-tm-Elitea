---
id: ELITEA-1833
title: "Upload Flow – Duplicate Handling: Close X Button on Resolve Duplicates Modal"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1833: Upload Flow – Duplicate Handling: Close X Button on Resolve Duplicates Modal

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X (close) button on the "Resolve duplicates" modal closes the modal without uploading any file and leaves the original file unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" already contains "sample.txt".
- A local file named "sample.txt" is available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Duplicate file | sample.txt |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list that already contains "sample.txt" | Bucket is selected |
| 3 | Click the upload icon in the top-right corner of the main panel | System file explorer opens |
| 4 | Verify the system file explorer opens immediately | File explorer is open |
| 5 | Select "sample.txt" and click "Open" | "Upload files to ..." modal opens |
| 6 | Verify the "Upload files to ..." modal opens and click "Upload" | Duplicate detection is triggered |
| 7 | Verify the "Resolve duplicates" modal opens listing "sample.txt" | Modal is visible with "sample.txt" listed |
| 8 | Click the X (close) icon in the top-right corner of the "Resolve duplicates" modal | Modal closes |
| 9 | Verify the modal is closed | Modal is no longer visible |
| 10 | Verify no file was uploaded and no success notification is displayed | No upload occurred; no notification shown |
| 11 | Verify the original "sample.txt" is unchanged in the file table | "sample.txt" remains with original metadata |

---

## Expected Final State

The "Resolve duplicates" modal is closed via the X button. No file is uploaded and the original "sample.txt" remains unchanged in the file table.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes via X button; no file uploaded; original file unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- File is uploaded after closing via X, or original file is modified.
