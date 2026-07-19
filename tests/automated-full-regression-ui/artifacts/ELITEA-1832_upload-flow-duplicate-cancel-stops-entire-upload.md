---
id: ELITEA-1832
title: "Upload Flow – Duplicate Handling: Cancel Stops Entire Upload Including Non-Duplicate Files"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
requirements: []
automation_test_id: tests.ui.artifacts.test_artifacts_upload_duplicate_cancel.TestArtifactUploadDuplicateCancel.test_cancel_stops_entire_upload_including_non_duplicate
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/635
---

# ELITEA-1832: Upload Flow – Duplicate Handling: Cancel Stops Entire Upload Including Non-Duplicate Files

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking "Cancel" in the "Resolve duplicates" modal stops the entire upload operation, including non-duplicate files, and leaves the bucket contents unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "sample.txt" but does NOT contain "sample.png".
- Note the current total number of files in "bucket-1".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Duplicate file | sample.txt |
| New file | sample.png |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list that already contains "sample.txt" but does NOT contain "sample.png" | Bucket is selected |
| 3 | Note the current total number of files in "bucket-1" | File count is recorded |
| 4 | Click the upload icon in the top-right corner of the main panel | System file explorer opens |
| 5 | Verify the system file explorer opens immediately | File explorer is open |
| 6 | Select both "sample.txt" (duplicate) and "sample.png" (new file) and click "Open" | Both files are selected |
| 7 | Verify the "Upload files to ..." modal opens with the Path field pre-filled with "bucket-1" | Modal is open |
| 8 | Click "Upload" | Duplicate detection is triggered |
| 9 | Verify the "Resolve duplicates" modal opens listing "sample.txt" as the duplicate file | Modal shows "sample.txt" as duplicate |
| 10 | Click "Cancel" | Cancel action completes |
| 11 | Verify the "Resolve duplicates" modal is closed | Modal is closed |
| 12 | Verify NO success notification is displayed | No success notification appears |
| 13 | Verify "sample.png" is NOT listed in the file table | "sample.png" was not uploaded |
| 14 | Verify the total number of files in "bucket-1" remains the same as noted in step 3 | File count is unchanged |
| 15 | Verify the original "sample.txt" is unchanged with its original "Last update" timestamp | Original file and timestamp are intact |

---

## Expected Final State

No files are uploaded after Cancel. The bucket contents and file count are identical to the state before the upload attempt. The "sample.txt" timestamp is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No files uploaded; bucket state is unchanged; no success notification shown.

**Fail:**
- Any step produces an error or unexpected result.
- "sample.png" is uploaded, or "sample.txt" is modified after Cancel.
