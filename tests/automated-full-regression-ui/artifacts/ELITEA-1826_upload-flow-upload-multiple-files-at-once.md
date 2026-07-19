---
id: ELITEA-1826
title: "Upload Flow – Upload Multiple Files at Once"
priority: high
type: functional
module: artifacts
status: ready
execution_type: automated
automation_test_id: tests.ui.artifacts.test_artifacts_upload_multiple_files.TestArtifactsUploadMultipleFiles.test_upload_multiple_files_at_once
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/647
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1826: Upload Flow – Upload Multiple Files at Once

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify that multiple files can be selected simultaneously in the file explorer and uploaded at once, with all files appearing in the file table after a single upload operation.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists.
- Test files "sample1.txt", "sample1.png", and "sample1.md" are available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Files to upload | sample1.txt, sample1.png, sample1.md |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Click the upload icon in the top-right corner of the main panel | System file explorer opens |
| 4 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 5 | Navigate to the test data folder and select multiple files at once: "sample1.txt", "sample1.png", "sample1.md" (use Ctrl+click or Shift+click) | All three files are selected |
| 6 | Click "Open" in the file explorer | "Upload files to ..." modal opens |
| 7 | Verify the "Upload files to ..." modal opens with the Path field pre-filled with "bucket-1" | Modal is open with correct path |
| 8 | Click "Upload" in the modal | Upload completes for all three files |
| 9 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 10 | Verify all three files — "sample1.txt", "sample1.png", "sample1.md" — are listed in the file table with Name, Type, Size and Last update values populated | All three files appear in the file table with metadata |

---

## Expected Final State

All three files are uploaded in a single operation and appear in the file table with correct metadata (name, type, size, last update).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All three files appear in the file table after a single multi-file upload.

**Fail:**
- Any step produces an error or unexpected result.
- Not all files are uploaded, or files are missing from the file table after upload.
