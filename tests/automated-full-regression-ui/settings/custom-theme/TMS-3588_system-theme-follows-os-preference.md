---
id: TMS-3588
title: "Selecting System theme follows OS dark/light preference"
priority: medium
type: functional
module: settings/preferences
status: ready
execution_type: manual
tags: [feat:settings, theme, system-theme, OS-preference]
requirements: []
---

# TMS-3588: Selecting System theme follows OS dark/light preference

**Module:** settings/preferences · **Priority:** medium · **Type:** functional

**Objective:** Verify that selecting "System" theme option causes ELITEA to follow the operating system's dark/light mode preference.

---

## Preconditions

- User is logged into ELITEA platform
- User has access to OS display/appearance settings
- User knows how to toggle OS dark/light mode
- Browser supports prefers-color-scheme media query

---

## Test Data

| Field | Value |
|-------|-------|
| OS Dark mode setting | System Preferences > Appearance > Dark |
| OS Light mode setting | System Preferences > Appearance > Light |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set OS to Dark mode | OS displays dark theme |
| 2 | Open ELITEA in browser | ELITEA loads |
| 3 | Navigate to Settings > Preferences | Preferences page loads |
| 4 | Select "System" theme option | System option is selected |
| 5 | Observe ELITEA UI | ELITEA displays dark theme matching OS |
| 6 | Open OS display settings | Settings panel opens |
| 7 | Change OS to Light mode | OS switches to light appearance |
| 8 | Return to ELITEA browser tab | ELITEA tab is focused |
| 9 | Observe ELITEA UI after OS change | ELITEA displays light theme matching OS |
| 10 | Toggle OS back to Dark mode | OS switches to dark appearance |
| 11 | Observe ELITEA UI | ELITEA switches to dark theme |

---

## Expected Final State

ELITEA automatically follows OS appearance preference when System theme is selected, switching between dark and light modes as OS setting changes.

---

## Pass/Fail Criteria

**Pass:**
- System option correctly detects OS preference
- Dark OS = Dark ELITEA theme
- Light OS = Light ELITEA theme
- Theme updates when OS preference changes (may require tab focus)

**Fail:**
- System option does not detect OS preference
- Theme doesn't match OS setting
- Theme doesn't update when OS changes
- Requires manual refresh to sync with OS
