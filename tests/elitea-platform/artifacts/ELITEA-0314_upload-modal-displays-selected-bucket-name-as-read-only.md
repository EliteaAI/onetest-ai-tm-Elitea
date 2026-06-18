---
id: ELITEA-0314
title: "Upload Modal Displays Selected Bucket Name as Read-Only"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [bucket-selection, artifacts, upload, modal, p0]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0314: Upload Modal Displays Selected Bucket Name as Read-Only

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the upload modal correctly pre-populates the bucket name from the context in which it was opened and does not allow the user to change it.

**Coverage:**
- Bucket name is pre-populated and shown in the upload modal
- Bucket field is read-only or non-editable
- Each bucket shows its own correct name when modal is opened from its context

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- At least one bucket exists in Artifacts (e.g., unicode-folder)

## Test Data

- URL: {{base_url}}
- Bucket: unicode-folder

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Select bucket 'unicode-folder'. | Bucket file list for 'unicode-folder' is displayed. |
| 2 | Click 'Upload files'. | Upload modal opens. |
| 3 | Verify the modal shows 'unicode-folder' as the selected bucket name. | Bucket name 'unicode-folder' is displayed in the modal. |
| 4 | Attempt to edit or clear the bucket name field. | The field is read-only or non-editable. No changes can be made to the bucket name. |
| 5 | Close the modal. If a second bucket exists, select it and reopen the upload modal. | The modal shows the second bucket's name correctly. |

## Expected Final State

The modal shows the second bucket's name correctly.

## Pass/Fail Criteria

**Pass:**
- Bucket name is correctly pre-populated in the upload modal
- Bucket field cannot be edited or changed from within the modal
- Each bucket shows its own name when the modal is opened from its context

**Fail:**
- Bucket name is not shown or is incorrect in the modal
- User is able to change the bucket name from within the modal
- Modal shows a wrong bucket name
