---
id: ELITEA-1827
title: "Upload Flow – Upload File to Nested Subfolder Path (Non-Existing Folder)"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
automation_test_id: tests.ui.artifacts.test_artifacts_upload_three_options_verify_selection.TestArtifactsUploadThreeOptionsVerifySelection.test_upload_via_three_options_and_verify_selection
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/658
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1827: Upload Flow – Upload File to Nested Subfolder Path (Non-Existing Folder)

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that entering a nested subfolder path in the Upload modal automatically creates all intermediate folders and uploads the file to the correct nested location.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists.
- Test file "sample.txt" is available for upload.
- Subfolders "folder-a" and "folder-b" do not yet exist in "bucket-1".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Upload path | bucket-1/folder-a/folder-b |
| Upload file | sample.txt |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list | Bucket is selected |
| 3 | Click the upload icon in the top-right corner of the main panel | System file explorer opens |
| 4 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 5 | Select file "sample.txt" and click "Open" | "Upload files to ..." modal opens |
| 6 | Verify the "Upload files to ..." modal opens | Modal is visible |
| 7 | Clear the Path field and enter: "bucket-1/folder-a/folder-b" | Path field shows "bucket-1/folder-a/folder-b" |
| 8 | Click "Upload" | Upload completes |
| 9 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 10 | Verify in the left panel "bucket-1" expands and shows "folder-a" as a subfolder | "folder-a" is visible under "bucket-1" |
| 11 | Verify "folder-a" expands and shows "folder-b" as a nested subfolder | "folder-b" is visible under "folder-a" |
| 12 | Click on "folder-b" in the left panel | "folder-b" is selected |
| 13 | Verify the main panel header displays "bucket-1 > folder-a > folder-b" | Breadcrumb shows full nested path |
| 14 | Verify "sample.txt" is listed in the file table inside "folder-b" | "sample.txt" is listed in the correct nested folder |

---

## Expected Final State

The nested folder structure "bucket-1/folder-a/folder-b" is automatically created during upload. "sample.txt" is accessible at the correct nested path.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Nested folders are auto-created and file is accessible at the correct path.

**Fail:**
- Any step produces an error or unexpected result.
- Nested folders are not created, or file is uploaded to the wrong location.
