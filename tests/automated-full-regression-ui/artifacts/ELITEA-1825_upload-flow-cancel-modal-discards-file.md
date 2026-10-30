---
id: ELITEA-1825
title: "Upload Flow: Cancel modal and Close X button discard file selection"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1825: Upload Flow: Cancel modal and Close X button discard file selection

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking Cancel on the upload modal or Close (X) on the duplicate resolution modal properly discards file selection without uploading, and no success notification is shown.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists.
- Test file "sample1.txt" is available for upload.
- Bucket "bucket-1" already contains "duplicate.txt".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File for cancel test | sample1.txt |
| Duplicate file | duplicate.txt |

---

## Steps

### Part 1: Cancel Upload Modal

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts section | Artifacts page loads |
| 2 | Click on "bucket-1" in bucket list | Bucket is selected |
| 3 | Click upload icon in top-right corner | System file explorer opens |
| 4 | Select "sample1.txt" and click Open | "Upload files to..." modal opens with path pre-filled |
| 5 | Verify modal is open with Path field populated | Modal visible with correct path |
| 6 | Click Cancel button | Modal closes |
| 7 | Verify modal is closed | Modal no longer visible |
| 8 | Verify "sample1.txt" is NOT listed in file table | File not uploaded |
| 9 | Verify no success notification is displayed | No notification appears |

### Part 2: Close X Button on Duplicate Resolution Modal

| # | Action | Expected Result |
|---|--------|-----------------|
| 10 | Click upload icon in top-right corner | System file explorer opens |
| 11 | Select "duplicate.txt" (same name as existing file) and click Open | "Upload files to..." modal opens |
| 12 | Verify path shows "bucket-1" | Modal shows correct path |
| 13 | Click Upload button | Duplicate detection triggers |
| 14 | Verify "Resolve duplicates" modal opens listing "duplicate.txt" | Duplicate resolution modal appears |
| 15 | Verify modal shows options: Skip, Replace, Keep both | All resolution options visible |
| 16 | Click X (close) button in top-right corner of modal | Modal closes |
| 17 | Verify duplicate resolution modal is closed | Modal no longer visible |
| 18 | Verify no success notification is displayed | No notification appears |
| 19 | Verify file table shows only original "duplicate.txt" (no new entry) | Only 1 "duplicate.txt" entry exists |
| 20 | Verify "Last update" timestamp of "duplicate.txt" is unchanged | Original timestamp intact |

---

## Expected Final State

- Upload modal Cancel: File not uploaded, no success notification
- Duplicate modal Close X: No upload occurs, original file unchanged, no new entries, no success notification

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both Cancel and Close X properly discard upload without notification; file table unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- File uploads despite Cancel/Close X, or success notification appears incorrectly.

---

## Notes

**Source functional tests:** ELITEA-1825, ELITEA-1833

**Regression rationale:** Consolidates upload cancellation behaviors (Cancel button on upload modal, Close X button on duplicate resolution modal) to verify both properly discard file selection.

**Selected checkpoints:**
- Upload modal Cancel discards selection (ELITEA-1825)
- Duplicate resolution modal Close X discards upload (ELITEA-1833)
- No success notification in either case
- File table remains unchanged
