---
id: ELITEA-1825
title: "Upload Flow – Cancel Upload Modal Discards File Selection"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1825: Upload Flow – Cancel Upload Modal Discards File Selection

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the "Upload files to ..." modal closes the modal without uploading the selected file and no success notification is shown.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists.
- Test file "sample1.txt" is available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File to select | sample1.txt |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Click the upload icon in the top-right corner of the main panel | System file explorer opens |
| 4 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 5 | Navigate to the test data folder and select file "sample1.txt" | "sample1.txt" is selected |
| 6 | Click "Open" in the file explorer | "Upload files to ..." modal opens |
| 7 | Verify the "Upload files to ..." modal opens with the Path field pre-filled | Modal is open with path pre-filled |
| 8 | Click "Cancel" in the modal | Modal closes |
| 9 | Verify the modal is closed | Modal is no longer visible |
| 10 | Verify "sample.txt" is NOT listed in the file table | No new file appeared in the file table |
| 11 | Verify no success notification is displayed | No success notification is shown |

---

## Expected Final State

The upload modal is closed by Cancel, no file is uploaded, and no success notification appears. The file table is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Modal closes on Cancel, file is not uploaded, and no success notification appears.

**Fail:**
- Any step produces an error or unexpected result.
- File is uploaded after Cancel, or success notification appears.
