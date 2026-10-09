---
id: ELITEA-1862
title: "File Preview/Edit – Image File Opens Directly as Image Preview with Inactive Edit Controls"
priority: medium
type: functional
module: artifacts
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.artifacts.test_artifacts_file_preview_image_restricted_controls.TestArtifactFilePreviewImageRestrictedControls.test_image_file_opens_directly_with_restricted_controls
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2398
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1862: File Preview/Edit – Image File Opens Directly as Image Preview with Inactive Edit Controls

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that an image file opens directly as a visual image preview in the editor panel, with Save/Discard buttons structurally absent (no edit path exists for images), no text editor, no Preview/Raw tabs, and an actions menu limited to Download and Delete.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "diagram (2).png".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | diagram (2).png |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and click on bucket "bucket-1" | Bucket is selected |
| 2 | Hover over file "diagram (2).png" in the left panel tree or file table | "View/Edit file" icon appears on hover |
| 3 | Verify a "View/Edit file" icon appears on hover | Icon is visible |
| 4 | Click on file "diagram (2).png" or its "View/Edit file" icon | Image preview opens in main panel |
| 5 | Verify the file opens in the main panel displaying the image directly | Image is displayed in the panel |
| 6 | Verify the panel header displays the full path: "bucket-1/diagram (2).png" | Header shows correct path |
| 7 | Verify the "Save" and "Discard" buttons in the top-right are not present | Both buttons are structurally absent — no edit path exists for an image file |
| 8 | Verify no "Preview" / "Raw" tabs are shown | No tabs are visible |
| 9 | Verify no text editor or content editing area is present — only the image is displayed | Only image is shown; no text editor |
| 10 | Verify the 3-dot (ellipsis) actions menu is present | Actions menu is accessible |
| 11 | Click the 3-dot menu — verify the dropdown contains only "Download" and "Delete" (no "Copy Content" option) | Only Download and Delete are shown |

---

## Expected Final State

Image file opens as a visual preview. Save/Discard are structurally absent (not merely disabled). No tabs or text editor shown. Actions menu contains only Download and Delete.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Image preview shown; Save/Discard structurally absent; no tabs; no text editor; actions limited to Download and Delete.

**Fail:**
- Any step produces an error or unexpected result.
- Save/Discard rendered in any form (active or disabled), text editor shown, tabs present, or "Copy Content" in actions menu.

---

## Adjustment history

- **2026-10-07 (ELITEA-1862 / EliteaAI/elitea-testing-public#2396, #2398):** Product change — for image files, the entire Save/Discard/Divider block in the preview header is now gated `canPreview && !isImageFileType` (`PreviewHeader.jsx`, EliteaUI `origin/main`), making the buttons structurally absent rather than present-and-disabled. Step 7 / Expected Final State / Pass-Fail Criteria updated to match current product behaviour. `automation_test_id` unchanged (same test, same path).
