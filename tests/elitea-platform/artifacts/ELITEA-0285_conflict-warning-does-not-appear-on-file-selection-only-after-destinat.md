---
id: ELITEA-0285
title: "Conflict Warning Does Not Appear on File Selection — Only After Destination Path Is Set"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:attachments, nfr:usability, eng:frontend, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4026]
---
# ELITEA-0285: Conflict Warning Does Not Appear on File Selection — Only After Destination Path Is Set

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting a file for upload does not immediately trigger a conflict check — the duplicate/conflict warning must only appear after the user has selected the destination path in the Upload Path Dialog.

**Coverage:**
- No conflict warning is shown at file selection time (before destination path is entered)
- Conflict warning is shown after a conflicting destination path is set
- Conflict warning is NOT shown when the destination path has no duplicate

## Preconditions

- Logged in to {{base_url}} as a user with artifacts.create permission
- A bucket named `test-bucket` exists in the Private project
- Subfolder `folder-a` exists in `test-bucket` and contains a file named `report.txt`
- Subfolder `folder-b` exists in `test-bucket` and does NOT contain a file named `report.txt`
- A local file named `report.txt` is available for upload

## Test Data

- Bucket: test-bucket
- Conflicting destination path: folder-a (contains report.txt)
- Non-conflicting destination path: folder-b (no report.txt)
- Upload file: report.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the sidebar. Select bucket 'test-bucket'. | Bucket file list for 'test-bucket' is displayed. |
| 2 | Click the Upload (cloud icon) button in the file table toolbar. | File browser opens. |
| 3 | Select the local file 'report.txt' from the file browser. | Upload Path Dialog opens showing the bucket name and an empty folder path input field. |
| 4 | Observe the Upload Path Dialog immediately after file selection, before typing any folder path. | No conflict or duplicate warning is displayed in the dialog. |
| 5 | Type 'folder-a' into the folder path input field. | Folder path field shows 'folder-a'. |
| 6 | Observe the Upload Path Dialog after setting 'folder-a' as the destination. | A conflict/duplicate warning appears listing 'report.txt' as an existing file in that path. |
| 7 | Clear the folder path field and type 'folder-b' instead. | Folder path field shows 'folder-b'. |
| 8 | Observe the Upload Path Dialog after setting 'folder-b' as the destination. | No conflict or duplicate warning is shown. |

## Expected Final State

No conflict or duplicate warning is shown.

## Pass/Fail Criteria

**Pass:**
- No warning visible at step 4 (immediately after file selection, before path entry)
- Conflict warning listing 'report.txt' is visible at step 6 (after 'folder-a' is entered)
- No warning visible at step 8 (after switching to non-conflicting 'folder-b')

**Fail:**
- A conflict warning appears at step 4 before any destination path is entered (premature trigger — old behavior)
- No warning appears at step 6 when the conflicting path 'folder-a' is set
- Warning persists at step 8 after switching to the non-conflicting path 'folder-b'
