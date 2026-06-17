---
id: ELITEA-0315
title: "Folder Path Input Validation - Invalid Patterns Are Rejected"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [folder-path, validation, artifacts, upload, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0315: Folder Path Input Validation - Invalid Patterns Are Rejected

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the folder path input field rejects invalid path patterns and disables the upload action until the input is corrected.

**Coverage:**
- Path starting with / triggers validation error and disables upload
- Path ending with / triggers validation error and disables upload
- Path containing // triggers validation error and disables upload
- Correcting to a valid path removes the error and re-enables upload

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- Upload modal is open with at least one file selected

## Test Data

- URL: {{base_url}}
- Invalid path 1: /invalid (leading slash)
- Invalid path 2: invalid/ (trailing slash)
- Invalid path 3: invalid//folder (consecutive slashes)
- Valid path: valid/path

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the upload modal for any bucket. Select a file. | Modal is open with a file ready to upload. |
| 2 | Enter folder path: /invalid (leading slash). | A validation error message is displayed. Upload button is disabled. |
| 3 | Clear the field. Enter folder path: invalid/ (trailing slash). | A validation error message is displayed. Upload button is disabled. |
| 4 | Clear the field. Enter folder path: invalid//folder (consecutive slashes). | A validation error message is displayed. Upload button is disabled. |
| 5 | Clear the field. Enter folder path: valid/path. | No validation error is shown. Upload button becomes enabled. |

## Expected Final State

No validation error is shown. Upload button becomes enabled.

## Pass/Fail Criteria

**Pass:**
- All three invalid path patterns trigger a visible validation error message
- Upload button is disabled for each invalid input
- Correcting to a valid path clears the error and enables the upload button

**Fail:**
- Any invalid path pattern passes validation without an error
- Upload button remains enabled for invalid input
- No error message is displayed
- A valid path is incorrectly rejected
