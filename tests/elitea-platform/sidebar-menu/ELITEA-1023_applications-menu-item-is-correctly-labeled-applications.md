---
id: ELITEA-1023
title: "\"Applications\" Menu Item Is Correctly Labeled \"Applications\""
priority: high
type: functional
module: sidebar-menu
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1, 3846]
requirements: [ProjectAlita/projectalita.github.io#3846]
---
# ELITEA-1023: "Applications" Menu Item Is Correctly Labeled "Applications"

**Module:** Sidebar Menu · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Applications menu item displays the correct label "Applications" in the expanded sidebar and in the tooltip when collapsed, in both Dark and Light modes.

**Coverage:**
- Expanded sidebar shows label "Applications"
- Collapsed sidebar tooltip reads "Applications"
- Label is correct in Dark mode
- Label is correct in Light mode

## Preconditions

- User is logged in to ELITEA
- Access to a project where the Applications menu item is visible

## Test Data

- Expected label: "Applications"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a project where the Applications menu item is visible. Expand the sidebar. | Sidebar is expanded and shows text labels next to icons. |
| 2 | Locate the Applications menu item. Read the text label next to the icon. | Text label reads exactly "Applications". |
| 3 | Collapse the sidebar to icon-only mode. | Sidebar collapses, only icons are visible. |
| 4 | Hover over the Applications icon. | A tooltip appears. |
| 5 | Read the tooltip text. | Tooltip reads exactly "Applications". |
| 6 | Switch to Dark mode (if not already). Repeat steps 1–5. | Label and tooltip both read "Applications" in Dark mode. |
| 7 | Switch to Light mode. Repeat steps 1–5. | Label and tooltip both read "Applications" in Light mode. |

## Expected Final State

Label and tooltip both read "Applications" in Light mode.

## Pass/Fail Criteria

**Pass:**
- Text label reads exactly "Applications" in both expanded and collapsed states
- Tooltip reads "Applications" in both Dark and Light mode

**Fail:**
- Label shows a different name (old incorrect name or blank)
- Tooltip shows incorrect text or does not appear
