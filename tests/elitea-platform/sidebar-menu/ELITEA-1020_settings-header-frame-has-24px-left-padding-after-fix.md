---
id: ELITEA-1020
title: "Settings Header Frame Has 24px Left Padding After Fix"
priority: medium
type: functional
module: sidebar-menu
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1, 3846]
requirements: [ProjectAlita/projectalita.github.io#3846]
---
# ELITEA-1020: Settings Header Frame Has 24px Left Padding After Fix

**Module:** Sidebar Menu · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Settings header frame has exactly 24px left padding after the fix, in both Dark and Light modes.

**Coverage:**
- Settings header padding-left computed value is 24px
- Header content is not flush against left edge
- Padding is consistent in Dark and Light mode

## Preconditions

- User is logged in to ELITEA
- Browser: Chrome (latest) with DevTools available

## Test Data

- Expected computed padding-left: 24px

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the Settings icon in the sidebar to open Settings. | Settings panel opens. |
| 2 | Right-click on the Settings panel header element (the area containing the section title at the top of the panel). Click Inspect to open DevTools. | DevTools opens with the header element selected. |
| 3 | In the Computed CSS panel, locate padding-left. | padding-left value is displayed. |
| 4 | Confirm the value equals 24px. | Computed padding-left is exactly 24px. |
| 5 | Visually inspect the header: the title/text should have visible breathing room from the left edge of the Settings panel — it should NOT be flush/touching the panel edge. | Header text has visible left margin consistent with 24px. |
| 6 | Switch to Dark mode and repeat steps 1–5. | padding-left remains 24px in Dark mode. |
| 7 | Switch to Light mode and repeat steps 1–5. | padding-left remains 24px in Light mode. |

## Expected Final State

padding-left remains 24px in Light mode.

## Pass/Fail Criteria

**Pass:**
- Computed padding-left of Settings header is 24px in both themes
- Header title is visually offset from the left edge

**Fail:**
- padding-left is a value other than 24px (e.g., old value: 16px, 0px)
- Header text appears flush or cut against the left panel edge
