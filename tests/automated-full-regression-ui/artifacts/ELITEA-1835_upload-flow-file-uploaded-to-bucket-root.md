---
id: ELITEA-1835
title: "Upload Flow – File Uploaded to Bucket Root When Bucket (Not Subfolder) Is Selected"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
automation_test_id: tests.ui.artifacts.test_artifacts_upload_three_options_verify_selection.TestArtifactsUploadThreeOptionsVerifySelection.test_upload_via_three_options_and_verify_selection
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/675
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1835: Upload Flow – File Uploaded to Bucket Root When Bucket (Not Subfolder) Is Selected

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that when the bucket root (not a subfolder) is selected and upload is triggered via the bucket 3-dot menu, the upload modal pre-fills the path with the bucket root and the file is uploaded to the correct root location.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" exists with subfolder "a1".
- Test file "sample.png" is available for upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| Subfolder | a1 |
| Upload file | sample.png |
| Expected path in modal | bucket-1/ |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section in the left sidebar | Artifacts page loads |
| 2 | Click on "bucket-1" in the bucket list — verify "bucket-1" is highlighted at the root level | "bucket-1" is selected at root level |
| 3 | Verify the main panel header displays "bucket-1" (no subfolder path) | Breadcrumb shows "bucket-1" only |
| 4 | Hover over "bucket-1" in the left panel and click the 3-dot (ellipsis) / actions icon | Dropdown menu appears |
| 5 | Verify a dropdown menu appears with options including "Upload files" | Dropdown menu is visible |
| 6 | Click "Upload files" | System file explorer opens |
| 7 | Verify the system file explorer/Open dialog window opens immediately | File explorer is open |
| 8 | Navigate to the test data folder and select "sample.png" and click "Open" | "Upload files to ..." modal opens |
| 9 | Verify the "Upload files to ..." modal opens | Modal is visible |
| 10 | Verify the Path field displays "bucket-1/" (reflecting the bucket root, not any subfolder) | Path shows "bucket-1/" |
| 11 | Verify the modal description indicates files will be uploaded to "bucket-1/" | Description text is correct |
| 12 | Click "Upload" | Upload completes |
| 13 | Verify a success notification is displayed: "Your file(s) have been successfully uploaded!" | Success notification appears |
| 14 | Verify the main panel displays "bucket-1" root level contents | Root level is shown |
| 15 | Verify "sample.png" is listed in the file table at the root level of "bucket-1" | "sample.png" is at root level |
| 16 | Verify "sample.png" is NOT listed inside subfolder "a1" | "sample.png" is not in subfolder |
| 17 | In the left panel click on subfolder "a1" and verify "sample.png" is not present there | "sample.png" is absent from "a1" |

---

## Expected Final State

"sample.png" is uploaded to the root of "bucket-1" and is not present in subfolder "a1". The upload modal correctly pre-fills the root path when the bucket (not a subfolder) is selected.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- File is at bucket root; not in subfolder; path pre-fills as bucket root.

**Fail:**
- Any step produces an error or unexpected result.
- File is uploaded to wrong location, or path shows subfolder instead of root.
