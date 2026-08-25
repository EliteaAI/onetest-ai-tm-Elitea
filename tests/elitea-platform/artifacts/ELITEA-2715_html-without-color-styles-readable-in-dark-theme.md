---
id: ELITEA-2715
title: "HTML without color styles is readable in Dark theme"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4, bug:5926]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file without explicit color definitions is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | test_file_1_under_1mb.htm |
| Theme | Dark |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Theme | Theme settings page opens |
| 2 | Set theme to "Dark" | Dark theme is applied to UI |
| 3 | Navigate to Artifacts > html-htm | Folder contents display |
| 4 | Open test_file_1_under_1mb.htm | File opens in Canvas |
| 5 | Observe text visibility in Preview mode | Text is readable |
| 6 | Scroll through the entire document | All text areas are visible |
| 7 | Verify there are no visibility issues | No black-on-black text |

## Expected Final State

- Text is clearly visible and readable in Dark theme
- Text color is light/white (not black on dark background)
- Content is fully readable without straining

## Pass/Fail Criteria

**Pass:**
- All text is clearly visible in Dark theme
- No black-on-black or invisible text issues
- Text color contrasts well with dark background

**Fail:**
- Text is invisible or barely visible
- Black text appears on dark background
- User cannot read content in Dark theme

**Note:** This test validates the fix for bug #5926
