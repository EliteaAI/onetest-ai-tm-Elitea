---
id: ELITEA-2717
title: "File type shows Html (detected)"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML files (.html and .htm) are available in Artifacts

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files | Any .html file, any .htm file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Artifacts section | Artifacts page loads |
| 2 | Open any .html file from Artifacts | File opens in Canvas |
| 3 | Observe the file type indicator in Canvas header | Type indicator is visible |
| 4 | Verify the indicator shows "Html (detected)" | Correct type is displayed |
| 5 | Switch to Raw mode | Raw mode displays |
| 6 | Verify file type indicator still shows "Html (detected)" | Type persists across modes |
| 7 | Repeat steps 2-6 with a .htm file | Same behavior for .htm |

## Expected Final State

- File type "Html (detected)" is displayed for both .html and .htm files
- Type indicator is visible next to file name in both modes

## Pass/Fail Criteria

**Pass:**
- File type shows "Html (detected)" for .html files
- File type shows "Html (detected)" for .htm files
- Indicator appears in both Preview and Raw modes

**Fail:**
- File type is not detected or shows incorrect type
- Type indicator is missing
- Type indicator disappears when switching modes
