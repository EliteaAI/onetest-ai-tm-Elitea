---
id: ELITEA-0295
title: "File upload on a paginated Artifacts list shows upload feedback on page 1"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, nfr:usability, issue:3720, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3720]
---
# ELITEA-0295: File upload on a paginated Artifacts list shows upload feedback on page 1

**Module:** Artifacts · **Priority:** Medium · **Type:** Functional

## Preconditions

- User is authenticated at {{base_url}}
- An Artifacts bucket exists with enough files to produce at least 2 pages in the file list
- User is on page 2 (or any page beyond page 1) of the Artifacts file list

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts and open a bucket that has 2+ pages of files. |  |
| 2 | Navigate to page 1. | Page 1 of the file list is displayed. |
| 3 | Drag and drop or using the Upload button, upload a file onto the Artifacts area. | Upload starts. An upload indicator or animation is immediately visible on page 1. |
| 4 | Wait for the upload to complete. | Upload indicator disappears; the uploaded file appears in the list on the appropriate page.Success message is displayed |

## Expected Final State

Upload indicator disappears; the uploaded file appears in the list on the appropriate page.Success message is displayed

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
