---
id: ELITEA-4079
title: "Background Colors section expands and allows editing all 21+ color values"
priority: medium
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, background-colors]
requirements: []
---

# ELITEA-4079: Background Colors section expands and allows editing all 21+ color values

**Module:** admin-portal/custom-theme · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Background Colors section in Custom Theme can be expanded to reveal all configurable background color options and that each can be edited.

---

## Preconditions

- User has Admin role with access to Admin Portal
- User is on Custom Theme configuration page
- Background Colors section is visible

---

## Test Data

| Field | Value |
|-------|-------|
| Section indicator | 21/31 colors (or similar) |
| Test color value | #2A2A4A |
| Sample background fields | Page background, Card background, Modal background, etc. |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Portal > Features > Custom Theme | Custom Theme page loads |
| 2 | Locate "Background Colors" section | Section shows with color count indicator (e.g., 21/31 colors) |
| 3 | Click on Background Colors section header to expand | Section expands revealing all color fields |
| 4 | Count the number of configurable color fields | At least 21 color options are displayed |
| 5 | Locate a specific background color (e.g., Page background) | Color field is visible with picker and hex input |
| 6 | Click on the color picker for Page background | Color picker opens |
| 7 | Select a new color (#2A2A4A) | Color is selected |
| 8 | Verify hex input updates | Hex field shows #2A2A4A |
| 9 | Locate another background color (e.g., Card background) | Second color field is visible |
| 10 | Edit via hex input directly | Enter new hex value |
| 11 | Verify color swatch updates | Swatch reflects new color |
| 12 | Collapse the Background Colors section | Section collapses |
| 13 | Re-expand to verify edits retained | Edited values are preserved |
| 14 | Click "Save Changes" | Changes save successfully |

---

## Expected Final State

All 21+ background color options are accessible, editable via both color picker and hex input, and changes can be saved.

---

## Pass/Fail Criteria

**Pass:**
- Section expands to show all color fields
- At least 21 background colors are configurable
- Both color picker and hex input work
- Changes persist when section collapses/expands
- Changes save successfully

**Fail:**
- Section doesn't expand
- Fewer colors than indicated are shown
- Color picker or hex input non-functional
- Edits lost when collapsing section
