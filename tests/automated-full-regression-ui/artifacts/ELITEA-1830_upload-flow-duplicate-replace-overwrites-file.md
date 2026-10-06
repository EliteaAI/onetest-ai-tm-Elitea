---
id: ELITEA-1830
title: "Upload Flow – Duplicate Handling: Replace Overwrites Existing File"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1830: Upload Flow – Duplicate Handling: Replace Overwrites Existing File

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking "Replace" in the "Resolve duplicates" modal overwrites the existing file with the new one, resulting in only one entry and an updated "Last update" timestamp.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" already contains "sample.txt" with a known timestamp.
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
| 3 | Note the current "Last update" timestamp of "sample.txt" | Timestamp is recorded |
| 4 | Click the upload icon in the top-right corner of the main panel | System file explorer opens |
| 5 | Verify the system file explorer opens immediately | File explorer is open |
| 6 | Select "sample.txt" (same name as the existing file) and click "Open" | "Upload files to ..." modal opens |
| 7 | Verify the "Upload files to ..." modal opens with the Path field pre-filled with "bucket-1" | Modal is open |
| 8 | Click "Upload" | Duplicate detection is triggered |
| 9 | Verify the "Resolve duplicates" modal opens listing "sample.txt" as the duplicate file | Modal shows "sample.txt" as duplicate |
| 10 | Click "Replace" | Replace action completes |
| 11 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 12 | Verify only one "sample.txt" entry exists in the file table (no duplicate rows) | Exactly one "sample.txt" row is present |
| 13 | Verify the "Last update" timestamp for "sample.txt" has been updated to the current date and time | Timestamp is newer than the original |

---

## Expected Final State

The original "sample.txt" is replaced by the new upload. Only one entry exists and its "Last update" timestamp is updated.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Single entry remains with updated timestamp after Replace.

**Fail:**
- Any step produces an error or unexpected result.
- Two entries exist after Replace, or timestamp is not updated.
