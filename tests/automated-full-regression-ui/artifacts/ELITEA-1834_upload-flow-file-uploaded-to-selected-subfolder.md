---
id: ELITEA-1834
title: "Upload Flow – File Uploaded to Selected Subfolder When Using Bucket Actions Button"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:artifacts]
automation_test_id:
  - tests.ui.artifacts.test_artifacts_upload_to_selected_subfolder.TestArtifactUploadToSelectedSubfolder.test_upload_via_bucket_actions_lands_in_selected_subfolder
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1633
requirements: []
---

# ELITEA-1834: Upload Flow – File Uploaded to Selected Subfolder When Using Bucket Actions Button

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that when a subfolder is selected in the left panel tree and upload is triggered via the bucket 3-dot menu, the upload modal pre-fills the path with the selected subfolder path and the file is uploaded to the correct subfolder.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists with subfolder "a1".
- Test file "sample.txt" is available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| Upload file | sample.txt |
| Expected path in modal | bucket-1/a1/ |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list to expand it | "bucket-1" expands showing subfolder "a1" |
| 3 | Click on subfolder "a1" under "bucket-1" to select it | "a1" is selected |
| 4 | Verify "a1" is highlighted (active/selected state) in the left panel tree | "a1" shows highlighted state |
| 5 | Verify the main panel header displays "bucket-1 > a1" | Breadcrumb shows "bucket-1 > a1" |
| 6 | Hover over "bucket-1" in the left panel and click the 3-dot (ellipsis) / actions icon next to the bucket name | Dropdown menu appears |
| 7 | Verify a dropdown menu appears with options including "Upload files" | Dropdown menu is visible |
| 8 | Click "Upload files" | System file explorer opens |
| 9 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 10 | Navigate to the test data folder and select "sample.txt" and click "Open" | "Upload files to ..." modal opens |
| 11 | Verify the "Upload files to ..." modal opens | Modal is visible |
| 12 | Verify the Path field displays "bucket-1/a1/" (reflecting the currently selected subfolder) | Path shows "bucket-1/a1/" |
| 13 | Verify the modal description indicates files will be uploaded to "bucket-1/a1/" | Description text is correct |
| 14 | Click "Upload" | Upload completes |
| 15 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 16 | Verify the main panel remains on "bucket-1 > a1" view | Main panel still shows subfolder view |
| 17 | Verify "sample.txt" is listed in the file table inside subfolder "a1" | "sample.txt" is in subfolder "a1" |
| 18 | Verify "sample.txt" is NOT listed at the root level of "bucket-1" | "sample.txt" is not at root level |

---

## Expected Final State

The file is uploaded to the selected subfolder "a1", not to the bucket root. The upload modal correctly pre-fills the path based on the currently selected subfolder.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- File is uploaded to "a1" subfolder; path pre-fills correctly based on selection.

**Fail:**
- Any step produces an error or unexpected result.
- File is uploaded to wrong location, or path does not reflect subfolder selection.
