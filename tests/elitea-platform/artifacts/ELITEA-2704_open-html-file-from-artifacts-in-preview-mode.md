---
id: ELITEA-2704
title: "Open HTML file from Artifacts in Preview mode"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Artifacts bucket contains HTML files (e.g., html-htm/script folder)
- User has access to the Artifacts section

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Bucket | Elitea S3 storage |
| Folder path | html-htm > script |
| Test file | test_file_2_between_1_3mb_structured.htm |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts section from the main menu | Artifacts page loads with bucket list visible |
| 2 | Select bucket: "Elitea S3 storage" | Bucket expands showing folder structure |
| 3 | Navigate to folder: html-htm > script | Folder contents are displayed with HTML files |
| 4 | Click on HTML file `test_file_2_between_1_3mb_structured.htm` | Canvas/File Preview panel opens |
| 5 | Observe the Canvas panel state | File is displayed in Canvas mode |

## Expected Final State

- HTML file is open in Canvas mode
- "Preview" tab is selected by default
- "Html (detected)" is displayed in the file type indicator
- HTML content renders correctly showing formatted content
- "Raw" tab is visible and clickable
- File path breadcrumb shows: html-htm > script > [filename]

## Pass/Fail Criteria

**Pass:**
- File opens in Canvas without errors
- Preview tab is selected by default
- File type shows "Html (detected)"
- HTML content renders with proper formatting
- Raw tab is available for switching

**Fail:**
- File fails to open or shows error message
- Raw mode is selected by default instead of Preview
- File type is not detected as HTML
- Content displays as raw text instead of rendered HTML
