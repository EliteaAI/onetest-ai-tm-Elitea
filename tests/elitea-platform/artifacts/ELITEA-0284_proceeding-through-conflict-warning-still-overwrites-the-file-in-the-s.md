---
id: ELITEA-0284
title: "Proceeding Through Conflict Warning Still Overwrites the File in the Selected Destination"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:attachments, nfr:usability, eng:frontend, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4026]
---
# ELITEA-0284: Proceeding Through Conflict Warning Still Overwrites the File in the Selected Destination

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the validation timing change, clicking Proceed in the conflict warning dialog still successfully overwrites the existing file in the selected destination — the overwrite flow remains functional end-to-end.

**Coverage:**
- Conflict warning still appears when the destination path has a file with the same name
- Clicking Proceed confirms and completes the overwrite
- The file in the destination is replaced with the newly uploaded version
- No additional confirmation prompts appear after Proceed is clicked

## Preconditions

- Logged in to {{base_url}} as a user with artifacts.create permission
- A bucket named `test-bucket` exists in the Private project
- Subfolder `folder-a` exists in `test-bucket` and contains a file named `report.txt` with content "version 1"
- A local file named `report.txt` with different content ("version 2") is available for upload

## Test Data

- Bucket: test-bucket
- Destination path: folder-a
- Existing file: report.txt (content: "version 1")
- Upload file: report.txt (content: "version 2" — different content, same filename)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the sidebar. Select bucket 'test-bucket'. | Bucket file list for 'test-bucket' is displayed. |
| 2 | Click the Upload button and select the local 'report.txt' file (version 2 content). | Upload Path Dialog opens. |
| 3 | Enter 'folder-a' in the folder path input field. | Conflict warning appears in the dialog, listing 'report.txt' as an existing file in 'folder-a'. |
| 4 | Click 'Proceed' in the conflict warning dialog. | The conflict dialog closes and the upload proceeds without additional prompts. |
| 5 | Navigate into 'folder-a' and click the preview (eye) icon on 'report.txt'. | File preview opens and the content reflects 'version 2' — the overwrite was successful. |
| 6 | Review whether any additional confirmation prompts appeared during the upload after step 4. | No additional dialogs or confirmation prompts were shown — upload completed in a single Proceed click. |

## Expected Final State

No additional dialogs or confirmation prompts were shown — upload completed in a single Proceed click.

## Pass/Fail Criteria

**Pass:**
- Conflict warning appears at step 3 after destination path is set
- File content in 'folder-a' reflects "version 2" content after upload (overwrite succeeded)
- No additional confirmation prompts appeared after clicking Proceed

**Fail:**
- No conflict warning appears at step 3 (warning mechanism broken by the fix)
- File still shows original "version 1" content after upload (overwrite did not execute)
- Additional unexpected confirmation prompts appeared during the upload flow
