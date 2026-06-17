---
id: ELITEA-0292
title: "Upload of Files with Forbidden Characters (#, ~, Consecutive Dots) Is Blocked with a Clear Error and Does Not Freeze the UI"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3699]
---
# ELITEA-0292: Upload of Files with Forbidden Characters (#, ~, Consecutive Dots) Is Blocked with a Clear Error and Does Not Freeze the UI

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that uploading files whose names contain `#`, `~`, or consecutive dots (`..`) is rejected before the upload completes, a descriptive error message is shown, the UI does not freeze, and no rejected file appears in the bucket.

**Coverage:**
- Filenames with `#` are blocked (`test#.txt`, `testdoc#.txt`)
- Filename with leading `~` is blocked (`~test.txt`)
- Filename with trailing `~` is blocked (`test~.txt`)
- Filenames with consecutive dots are blocked (`tes..t.txt`, `file....txt`)
- Combined forbidden characters blocked (`test#~..combo.txt`)
- Error message references all restricted characters
- UI does not freeze or enter an indeterminate state after any rejection
- Error is dismissible and the upload button remains operational after rejection
- Valid baseline (`testfile.txt`) uploads successfully after rejection attempts

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome (latest)
- Bucket `tc-bucket` exists and is accessible
- User has `artifacts.create` and `configuration.artifacts.artifacts.view` permissions
- Test files prepared locally: `test#.txt`, `testdoc#.txt`, `~test.txt`, `test~.txt`, `tes..t.txt`, `file....txt`, `test#~..combo.txt`, `testfile.txt`

## Test Data

Bucket: tc-bucket
Forbidden files: test#.txt, testdoc#.txt, ~test.txt, test~.txt, tes..t.txt, file....txt, test#~..combo.txt
Valid baseline: testfile.txt
Expected error snippet: "Filenames cannot contain the following symbols: #, ~, .. Please rename your file and try again."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/ and open the Artifacts section. | Artifacts page is displayed with the bucket list. |
| 2 | Open `tc-bucket`. | Bucket contents page is displayed. |
| 3 | Click 'Upload files'; select `test#.txt` and confirm in the OS file chooser. | Validation runs; no upload starts; no spinner persists; `test#.txt` does NOT appear in the bucket list; a descriptive error message referencing `#` is displayed. |
| 4 | Dismiss the error; verify the 'Upload files' button is active. | Error dismissed without page reload; 'Upload files' button is clickable. |
| 5 | Click 'Upload files'; select `testdoc#.txt` and confirm. | `testdoc#.txt` does NOT appear in the bucket; error references `#`; no UI freeze. |
| 6 | Click 'Upload files'; select `~test.txt` and confirm. | `~test.txt` does NOT appear in the bucket; error references `~`; no UI freeze. |
| 7 | Click 'Upload files'; select `test~.txt` and confirm. | `test~.txt` does NOT appear in the bucket; error references `~`; no UI freeze. |
| 8 | Click 'Upload files'; select `tes..t.txt` and confirm. | `tes..t.txt` does NOT appear in the bucket; error references consecutive dots (`..`); no UI freeze. |
| 9 | Click 'Upload files'; select `file....txt` and confirm. | `file....txt` does NOT appear in the bucket; error references `..`; no UI freeze. |
| 10 | Click 'Upload files'; select `test#~..combo.txt` and confirm. | `test#~..combo.txt` does NOT appear in the bucket; error references `#`, `~`, and `..`; no UI freeze. |
| 11 | Read the full text of the error message shown in step 10. | Error message matches or includes: "Filenames cannot contain the following symbols: #, ~, .. Please rename your file and try again." |
| 12 | Click 'Upload files'; select `testfile.txt` and confirm. | Upload begins without a rejection error. |
| 13 | Observe the bucket file list. | `testfile.txt` appears in the bucket with a correct, non-zero file size. |

## Expected Final State

`testfile.txt` appears in the bucket with a correct, non-zero file size.

## Pass/Fail Criteria

**Pass:**
- All 7 forbidden-character files are blocked; none appear in the bucket file list
- Each rejection shows a descriptive error referencing the specific restricted character(s)
- No rejection causes a UI freeze, perpetual spinner, or disabled upload button
- Error is dismissible without a page reload after each rejection
- `testfile.txt` uploads successfully and appears with correct non-zero file size

**Fail:**
- Any forbidden-character file is accepted and appears in the bucket
- No error shown, or the error is generic with no reference to the restricted character(s)
- Any rejection freezes the UI or leaves the 'Upload files' button disabled
- `testfile.txt` fails to upload or the UI requires a page reload before it does
