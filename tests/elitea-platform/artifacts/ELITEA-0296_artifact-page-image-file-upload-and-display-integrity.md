---
id: ELITEA-0296
title: "Artifact Page – Image File Upload and Display Integrity"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0296: Artifact Page – Image File Upload and Display Integrity

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after the bug fix, image files can still be uploaded to an artifact bucket via the Artifacts page and are displayed correctly in the file list with correct name, type, and size metadata.

**Coverage:**
- .png image file uploads successfully via the Artifacts page
- .jpg image file uploads successfully via the Artifacts page
- Both files appear in the file list with correct name, type category, and file size
- Preview icon renders the image correctly for at least one uploaded image

## Preconditions

- Logged in to {{base_url}}
- User has artifacts.create permission
- An existing Artifact bucket is accessible
- Two sample image files are available for upload: test_upload.png and test_upload.jpg

## Test Data

- Files to upload: test_upload.png (any small PNG image), test_upload.jpg (any small JPEG image)
- Bucket: any existing accessible bucket
- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the sidebar. | Artifacts page loads showing the bucket list. |
| 2 | Select an existing bucket from the list. | Bucket file list is displayed. |
| 3 | Click Upload files and select test_upload.png and test_upload.jpg. | Both files are selected for upload. |
| 4 | Confirm the upload. | Upload completes. Both files appear in the file list. |
| 5 | Verify the file list entries for both files show: correct filename, type column value, and non-zero file size. | Both entries are correctly populated with accurate metadata. |
| 6 | Click the Preview icon for test_upload.png. | Image preview opens and renders the image correctly without errors. |

## Expected Final State

Image preview opens and renders the image correctly without errors.

## Pass/Fail Criteria

**Pass:**
- Both .png and .jpg files upload without errors
- Files appear in the file list with correct filename, type, and non-zero size
- Preview opens and renders the image correctly

**Fail:**
- Upload fails for .png or .jpg
- Files show incorrect type or zero size in the file list
- Preview fails to render the image
