---
id: ELITEA-0310
title: "Bucket File List Correctly Displays Folders Alongside Root-Level Files"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [folder-navigation, regression, file-list, artifacts, p1]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0310: Bucket File List Correctly Displays Folders Alongside Root-Level Files

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Artifacts bucket file list correctly renders both folder entries and root-level flat files as distinct, co-existing items with accurate pagination and counts.

**Coverage:**
- Folder entries and root-level files are displayed together in the list
- Folders are visually distinguishable from regular files
- Folder navigation (in and back to root) works correctly
- No duplicate entries exist; pagination count is accurate

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Bucket 'unicode-folder' contains: at least 2 root-level files and 1 subfolder (another_folder) with files inside

## Test Data

- URL: {{base_url}}
- Bucket: unicode-folder
- Root files: testdoc#.txt, ts upload 02.txt
- Subfolder: another_folder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select bucket 'unicode-folder'. | File list is displayed showing both files and folder entries. |
| 2 | Verify root-level files (e.g., testdoc#.txt, ts upload 02.txt) appear in the list. | Root files are visible at the top level. |
| 3 | Verify 'another_folder' appears as a folder entry with a distinct icon or styling. | Folder is listed and visually distinguishable from files. |
| 4 | Click into 'another_folder'. | Folder opens and shows its contents. |
| 5 | Navigate back to the bucket root using breadcrumb or back navigation. | File list returns to bucket root, showing folders and root files with no duplicates. Pagination count reflects the correct total. |

## Expected Final State

File list returns to bucket root, showing folders and root files with no duplicates. Pagination count reflects the correct total.

## Pass/Fail Criteria

**Pass:**
- Folders and root-level files are displayed together without conflicts
- Folders are visually distinguishable from files (folder icon or distinct styling)
- Folder navigation works in both directions (into and back to root)
- No duplicate entries; file count in pagination is accurate

**Fail:**
- Folder entries are missing or shown as regular files
- Root-level files disappear after a folder is present
- Duplicate entries appear in the list
- Navigation back to root fails or shows incorrect content
