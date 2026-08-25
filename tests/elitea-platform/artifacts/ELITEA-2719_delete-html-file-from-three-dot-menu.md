---
id: ELITEA-2719
title: "Delete HTML file from three-dot menu"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Test HTML file exists in Artifacts (create a copy for testing)
- User has delete permission

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | A test copy of HTML file (not critical data) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or identify a test HTML file in Artifacts | Test file is ready |
| 2 | Open the HTML file in Canvas | File opens in Canvas |
| 3 | Click three-dot menu in top-right corner | Menu dropdown appears |
| 4 | Click "Delete" option | Confirmation dialog appears |
| 5 | Observe the confirmation dialog | Dialog asks for confirmation |
| 6 | Click "Cancel" to abort first | Dialog closes, file remains |
| 7 | Click Delete again and confirm deletion | File is deleted |
| 8 | Navigate to Artifacts folder where file was located | Folder contents display |
| 9 | Verify file no longer appears | File is removed from list |

## Expected Final State

- File is deleted from Artifacts
- Canvas closes after deletion
- File no longer appears in the folder

## Pass/Fail Criteria

**Pass:**
- Delete option triggers confirmation dialog
- Cancel aborts the deletion
- Confirming deletion removes the file
- File no longer appears in Artifacts

**Fail:**
- Delete option is missing or disabled
- No confirmation dialog appears
- File remains after confirming deletion

**Note:** Use a test copy file to avoid losing important files
