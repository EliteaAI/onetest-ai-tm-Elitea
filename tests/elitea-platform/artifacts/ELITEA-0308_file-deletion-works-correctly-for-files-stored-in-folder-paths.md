---
id: ELITEA-0308
title: "File Deletion Works Correctly for Files Stored in Folder Paths"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0308: File Deletion Works Correctly for Files Stored in Folder Paths

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Delete action correctly removes a file stored under a folder path without affecting sibling files or other bucket contents.

**Coverage:**
- File deletion works for files stored under a folder prefix
- Deleting one file does not remove sibling files in the same folder
- Root-level files in the same bucket are unaffected by folder-level deletions

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Folder 'test' in the bucket contains at least two files: fileA.txt and fileB.txt
- Bucket also contains at least one root-level file

## Test Data

- URL: {{base_url}}
- Folder: test
- Files in folder: fileA.txt (to delete), fileB.txt (to remain)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select the bucket. Navigate into folder 'test'. | Folder contents are displayed with both fileA.txt and fileB.txt. |
| 2 | Select fileA.txt and click the Delete action. Confirm deletion. | fileA.txt is removed from the folder list. |
| 3 | Verify fileB.txt is still present in the folder. | fileB.txt remains listed and is accessible. |
| 4 | Navigate back to the bucket root. | Root-level files are still present and the folder 'test' entry is still visible (if it still contains files). |
| 5 | Preview and Download fileB.txt to confirm it is intact. | fileB.txt opens and downloads correctly. |

## Expected Final State

fileB.txt opens and downloads correctly.

## Pass/Fail Criteria

**Pass:**
- Selected file is successfully deleted from the folder
- Sibling file in the same folder remains intact
- Root-level files in the same bucket are unaffected

**Fail:**
- File deletion fails for folder-path files
- Sibling file is unexpectedly deleted or moved
- Root-level files are affected by the deletion
