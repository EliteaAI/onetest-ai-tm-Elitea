---
id: TMS-3558
title: "Delete Theme resets custom theme configuration to default values"
priority: medium
type: functional
module: admin-portal/custom-theme
status: ready
execution_type: manual
tags: [feat:admin, feat:custom-theme, delete, reset]
requirements: []
---

# TMS-3558: Delete Theme resets custom theme configuration to default values

**Module:** admin-portal/custom-theme · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Delete Theme functionality resets all custom theme configuration to default values, removing custom colors and uploaded logo.

---

## Preconditions

- User has Admin role with access to Admin Portal
- Custom theme has been configured with non-default values:
  - Custom Primary colors set
  - Custom logo uploaded (optional)
  - Other color sections modified
- Changes have been saved

---

## Test Data

| Field | Value |
|-------|-------|
| Pre-delete Primary Main | Custom color (e.g., #FF5733) |
| Post-delete Primary Main | Default color |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Portal > Features > Custom Theme | Custom Theme page loads |
| 2 | Verify custom values are currently configured | Primary Colors show non-default values |
| 3 | Note current Primary Main color value | Custom color is recorded |
| 4 | Note if custom logo is uploaded | Logo presence is recorded |
| 5 | Locate "Delete Theme" button (red/destructive styling) | Delete Theme button is visible |
| 6 | Click "Delete Theme" button | Confirmation dialog may appear |
| 7 | Confirm deletion if prompted | Deletion proceeds |
| 8 | Observe Primary Colors section | Colors reset to default values |
| 9 | Observe Platform Logo section | Logo upload area shows empty/default state |
| 10 | Observe other color sections | All sections show default values |
| 11 | Refresh the page | Page reloads |
| 12 | Verify all values remain at defaults | No custom values restored |
| 13 | Switch to user view and select Project theme | Project theme is selected |
| 14 | Verify default appearance is shown | No custom styling visible |

---

## Expected Final State

All custom theme configuration is reset to defaults: colors return to base values, uploaded logo is removed, and users see default appearance.

---

## Pass/Fail Criteria

**Pass:**
- Delete Theme button is accessible
- Confirmation is shown before destructive action
- All color values reset to defaults
- Uploaded logo is removed
- Defaults persist after refresh
- Users see default theme when selecting Project

**Fail:**
- Delete button not functional
- No confirmation before deletion
- Some custom values retained after delete
- Logo remains after deletion
- Defaults don't persist
