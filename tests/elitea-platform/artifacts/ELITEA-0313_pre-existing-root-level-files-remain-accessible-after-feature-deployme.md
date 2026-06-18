---
id: ELITEA-0313
title: "Pre-Existing Root-Level Files Remain Accessible After Feature Deployment"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [backward-compatibility, regression, artifacts, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0313: Pre-Existing Root-Level Files Remain Accessible After Feature Deployment

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that files previously uploaded directly to the bucket root (without any folder path) remain visible, previewable, and downloadable after the folder-path upload feature is deployed.

**Coverage:**
- Pre-existing root-level files still appear in the file list
- Preview action works correctly for pre-existing root files
- Download action works correctly for pre-existing root files
- No data loss or file misclassification introduced by the new feature

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Bucket 'unicode-folder' contains at least 3 root-level files pre-existing before the feature deployment (e.g., testdoc#.txt, ts upload 02.txt, New Text Document111.txt)

## Test Data

- URL: {{base_url}}
- Bucket: unicode-folder
- Pre-existing root files: testdoc#.txt, ts upload 02.txt, New Text Document111.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select the bucket with pre-existing root-level files. | File list is displayed with existing files visible. |
| 2 | Verify pre-existing files (testdoc#.txt, ts upload 02.txt, New Text Document111.txt) appear in the list without any folder prefix or unexpected grouping. | All pre-existing files are listed at root level. |
| 3 | Click Preview on one pre-existing file. | File preview opens and displays content correctly. No 404 or permission error. |
| 4 | Select a pre-existing file and click Download. | File downloads successfully. Content is intact. |
| 5 | Upload a new file with folder path test/new.txt. Return to bucket root and verify pre-existing files are still listed and unaffected. | Pre-existing root files remain present and all actions continue to work correctly. |

## Expected Final State

Pre-existing root files remain present and all actions continue to work correctly.

## Pass/Fail Criteria

**Pass:**
- All pre-existing root-level files remain visible in the bucket file list
- Preview and Download actions work correctly for pre-existing files
- New folder-path uploads do not affect pre-existing root files

**Fail:**
- Any pre-existing root-level files are missing from the list
- Preview or Download fails for pre-existing files
- Pre-existing files are moved into a folder unintentionally
