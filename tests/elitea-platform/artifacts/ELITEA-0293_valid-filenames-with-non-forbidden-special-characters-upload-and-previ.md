---
id: ELITEA-0293
title: "Valid Filenames with Non-Forbidden Special Characters Upload and Preview Correctly"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3699]
---
# ELITEA-0293: Valid Filenames with Non-Forbidden Special Characters Upload and Preview Correctly

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the new filename validation logic does not over-block filenames containing non-restricted characters (spaces, `@`, `!`, Unicode/CJK, hyphens, underscores, parentheses), and that these files upload and preview successfully without errors.

**Coverage:**
- `ts uplo@ad @!.txt` (spaces, `@`, `!`) uploads and previews correctly
- `New Text 子.txt` (Unicode/CJK) uploads and previews correctly
- `test-file_v2.txt` (hyphen, underscore) uploads and previews correctly
- `report (final).txt` (parentheses, spaces) uploads and previews correctly
- All files appear in bucket with correct non-zero file size (no `-` size anomaly)
- No forbidden-character error shown for any of these files

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome (latest)
- Bucket `tc-bucket` accessible
- User has `artifacts.create` and `configuration.artifacts.artifacts.view` permissions
- Test files prepared locally: `ts uplo@ad @!.txt`, `New Text 子.txt`, `test-file_v2.txt`, `report (final).txt`

## Test Data

Bucket: tc-bucket
Valid filenames:
  ts uplo@ad @!.txt    -> spaces, @, !
  New Text 子.txt      -> Unicode/CJK character
  test-file_v2.txt     -> hyphen, underscore
  report (final).txt   -> parentheses, spaces

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/ and open the Artifacts section. | Artifacts page is displayed. |
| 2 | Open `tc-bucket`. | Bucket contents page is displayed. |
| 3 | Click 'Upload files'; select `ts uplo@ad @!.txt` and confirm. | Upload begins; no forbidden-character error shown; `ts uplo@ad @!.txt` appears in the bucket with a correct, non-zero file size. |
| 4 | Click 'Upload files'; select `New Text 子.txt` and confirm. | Upload begins; no forbidden-character error shown; `New Text 子.txt` appears in the bucket with a correct, non-zero file size. |
| 5 | Click 'Upload files'; select `test-file_v2.txt` and confirm. | Upload begins; no forbidden-character error shown; `test-file_v2.txt` appears in the bucket with a correct, non-zero file size. |
| 6 | Click 'Upload files'; select `report (final).txt` and confirm. | Upload begins; no forbidden-character error shown; `report (final).txt` appears in the bucket with a correct, non-zero file size. |
| 7 | Click the Preview (eye icon) next to `ts uplo@ad @!.txt`. | Preview panel opens; file content loads without error; no forbidden-character error message shown. |
| 8 | Close the preview; click the Preview icon next to `New Text 子.txt`. | Preview panel opens; file content loads without error; no forbidden-character error message shown. |
| 9 | Close the preview; click the Preview icon next to `test-file_v2.txt`. | Preview panel opens; file content loads without error; no forbidden-character error message shown. |
| 10 | Close the preview; click the Preview icon next to `report (final).txt`. | Preview panel opens; file content loads without error; no forbidden-character error message shown. |

## Expected Final State

Preview panel opens; file content loads without error; no forbidden-character error message shown.

## Pass/Fail Criteria

**Pass:**
- All 4 valid files upload successfully with no forbidden-character error
- Each appears in the bucket with correct non-zero file size (no `-` anomaly)
- Preview of each file loads content without any forbidden-character error

**Fail:**
- Any valid file is incorrectly blocked with a forbidden-character error
- Any file shows missing, zero, or `-` file size after uploading
- Preview of any valid file triggers a forbidden-character error or fails to load content
