---
id: TMS-3553
title: "Theme selection persists after page refresh via localStorage"
priority: high
type: functional
module: settings/preferences
status: ready
execution_type: manual
tags: [feat:settings, theme, persistence, localStorage]
requirements: []
---

# TMS-3553: Theme selection persists after page refresh via localStorage

**Module:** settings/preferences · **Priority:** high · **Type:** functional

**Objective:** Verify that the user's theme selection is saved to localStorage and persists across page refreshes and browser sessions.

---

## Preconditions

- User is logged into ELITEA platform
- Browser localStorage is enabled (not in strict privacy mode)
- User has access to Settings > Preferences

---

## Test Data

| Field | Value |
|-------|-------|
| localStorage key | mode (or theme-related key) |
| Test themes | Dark, Light, Project |

---

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings > Preferences | Preferences page loads |
| 2 | Note current theme selection | Current theme is observed |
| 3 | Select "Dark" theme | Dark theme is applied |
| 4 | Refresh the page (F5 or Ctrl+R) | Page reloads |
| 5 | Verify Dark theme is still active | Dark theme persists after refresh |
| 6 | Navigate to Settings > Preferences | Preferences page loads |
| 7 | Verify "Dark" option is shown as selected | Dark option is highlighted/selected |
| 8 | Select "Project" theme | Project theme is applied |
| 9 | Close browser tab completely | Tab closes |
| 10 | Open new tab and navigate to ELITEA | ELITEA loads in new tab |
| 11 | Verify Project theme is active | Project theme persists across tabs |
| 12 | Open browser DevTools > Application > localStorage | DevTools opens |
| 13 | Verify theme/mode value is stored | localStorage contains theme setting |

---

## Expected Final State

Theme selection is stored in localStorage and automatically applied on subsequent page loads without requiring user to re-select.

---

## Pass/Fail Criteria

**Pass:**
- Theme persists after page refresh
- Theme persists after closing and reopening tab
- localStorage contains theme value
- Correct theme option shown as selected in Preferences

**Fail:**
- Theme resets to default after refresh
- localStorage doesn't contain theme value
- Selected theme doesn't match visual appearance
- Theme lost when opening new tab
