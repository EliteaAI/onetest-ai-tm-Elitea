---
id: TMS-3549
title: "User can see all 4 theme options in Preferences: System, Dark, Light, Project"
priority: high
type: functional
module: settings/preferences
status: ready
execution_type: manual
tags: [feat:settings, feat:custom-theme, theme-selector]
requirements: []
---

# TMS-3549: User can see all 4 theme options in Preferences: System, Dark, Light, Project

**Module:** settings/preferences · **Priority:** high · **Type:** functional

**Objective:** Verify that the Theme selector in user Preferences displays all four available theme options: System, Dark, Light, and Project.

---

## Preconditions

- User is logged into ELITEA platform
- User has access to Settings > Preferences
- Custom Theme feature is enabled for the environment

---

## Test Data

| Field | Value |
|-------|-------|
| Expected theme options | System, Dark, Light, Project |
| Navigation path | Settings > Preferences |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in to ELITEA platform | User is authenticated and lands on dashboard |
| 2 | Click "Settings" in the left sidebar | Settings page opens |
| 3 | Click "Preferences" in the settings menu | Preferences page loads |
| 4 | Locate the "GENERAL" section | General section is visible at top |
| 5 | Locate the "Theme" row | Theme selector is displayed |
| 6 | Verify "System" option is present | System option visible with appropriate icon |
| 7 | Verify "Dark" option is present | Dark option visible with moon/dark icon |
| 8 | Verify "Light" option is present | Light option visible with sun/light icon |
| 9 | Verify "Project" option is present | Project option visible (may show "Project theme" label) |
| 10 | Verify all options are clickable/selectable | Each option responds to click/hover |

---

## Expected Final State

All four theme options (System, Dark, Light, Project) are displayed in the Theme selector and are interactive.

---

## Pass/Fail Criteria

**Pass:**
- All 4 theme options are visible
- Each option has appropriate label and icon
- Options are clickable and respond to interaction
- Layout is consistent and accessible

**Fail:**
- Any theme option is missing
- Options are not clickable
- Labels are incorrect or icons missing
- Project option not available when custom theme is configured
