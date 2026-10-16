---
id: ELITEA-3997
title: "All Sections Display Correctly in Dark and Light Themes"
priority: medium
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, themes, accessibility]
requirements: [EL-6252]
---
# ELITEA-3997: All Sections Display Correctly in Dark and Light Themes

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that Configuration, Tools, and Indexes sections display correctly with proper contrast and visibility in both dark and light themes.

**Coverage:**
- All sections readable in dark theme
- All sections readable in light theme
- Icons visible and distinguishable in both themes
- Counts, warnings, and status indicators properly visible
- Form controls (dropdowns, toggles) usable in both themes

## Preconditions

- Logged in to {{base_url}}
- A toolkit with Configuration, Tools, and Indexes sections
- Ability to switch between dark and light themes

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any existing toolkit with tools and indexes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ensure application is in Dark theme (default). | Dark theme active. |
| 2 | Navigate to Toolkits & Indexes → open any toolkit. | Toolkit details page opens. |
| 3 | Verify Configuration section is readable. | Text, labels, form fields have sufficient contrast. |
| 4 | Verify "Show more/less" link is visible. | Link clearly visible and styled. |
| 5 | Verify view mode icons are visible. | Form/Raw JSON icons distinguishable. |
| 6 | Expand Tools section and verify readability. | Tool names, toggles, counts clearly visible. |
| 7 | Verify tool count in header is readable. | "16 / 33" format clearly visible. |
| 8 | Expand Indexes section and verify readability. | Index cards, counts, status indicators visible. |
| 9 | Switch to Light theme (via Settings or theme toggle). | Application switches to light theme. |
| 10 | Verify Configuration section in light theme. | All elements readable with good contrast. |
| 11 | Verify Tools section in light theme. | Counts, toggles, tool names clearly visible. |
| 12 | Verify Indexes section in light theme. | Index cards, status indicators visible. |
| 13 | Switch back to Dark theme. | All elements adapt correctly to dark theme. |

## Expected Final State

All toolkit sections display correctly with proper contrast, visibility, and usability in both dark and light themes.

## Pass/Fail Criteria

**Pass:**
- All text readable in both themes
- Icons visible and distinguishable
- Form controls (dropdowns, toggles) usable
- Counts and indicators clearly visible
- No contrast issues in either theme

**Fail:**
- Text unreadable or low contrast
- Icons invisible or indistinguishable
- Form controls hard to see or use
- Counts or indicators not visible
