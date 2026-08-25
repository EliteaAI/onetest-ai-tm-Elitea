---
id: ELITEA-2718
title: "Open htm file with alternate extension"
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
- Artifacts bucket contains .htm files

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | test_file_3_greater_5mb.htm |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts > html-htm > script | Folder contents display |
| 2 | Locate a .htm file | File is visible in list |
| 3 | Click to open the .htm file | File opens in Canvas |
| 4 | Verify file type shows "Html (detected)" | Type is correctly identified |
| 5 | Verify Preview mode works | HTML content renders |
| 6 | Switch to Raw mode | Source code displays |
| 7 | Verify Raw mode works identically to .html files | Full functionality available |

## Expected Final State

- .htm file opens in Canvas same as .html
- File type shows "Html (detected)"
- Preview and Raw modes work identically to .html files

## Pass/Fail Criteria

**Pass:**
- .htm file opens without errors
- Treated identically to .html files
- File type correctly detected as HTML
- All features work (Preview, Raw, Edit, Save)

**Fail:**
- .htm file fails to open
- File type not detected correctly
- Features work differently than .html
