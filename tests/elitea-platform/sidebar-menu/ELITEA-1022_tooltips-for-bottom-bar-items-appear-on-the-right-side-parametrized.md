---
Deprecate
id: ELITEA-1022
title: "Tooltips for Bottom-Bar Items Appear on the Right Side [Parametrized]"
priority: high
type: functional
module: sidebar-menu
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1, 3846]
requirements: [ProjectAlita/projectalita.github.io#3846]
---
# ELITEA-1022: Tooltips for Bottom-Bar Items Appear on the Right Side [Parametrized]

**Module:** Sidebar Menu · **Priority:** High · **Type:** Functional

**Objective:** Verify that tooltips for Agent Studio, Settings, Tips, Notifications, and User Profile all appear to the right of their icons after the tooltip position fix.

**Coverage:**
- Agent Studio tooltip positioned right
- Settings tooltip positioned right
- Tips tooltip positioned right
- Notifications tooltip positioned right
- User Profile tooltip positioned right
- Tooltip appears and disappears cleanly on hover/hover-out
- Tooltip text is correct for each item

## Preconditions

- User is logged in to ELITEA
- Sidebar is in collapsed (icon-only) mode

## Test Data

| # | Item | Expected Tooltip Text |
|---|---|---|
| 1 | Agent Studio | "Agent Studio" |
| 2 | Settings | "Settings" |
| 3 | Tips | "Tips" |
| 4 | Notifications | "Notifications" |
| 5 | User Profile | User name or "Profile" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Collapse the sidebar to icon-only mode (if expanded, click the ELITEA logo). | Sidebar shows icons only, no text labels. |
| 2 | Hover over the Agent Studio icon (bottom bar). | Tooltip appears to the right side of the icon. Tooltip text is "Agent Studio". |
| 3 | Move the cursor away. | Tooltip disappears cleanly. |
| 4 | Hover over the Settings icon. | Tooltip appears to the right side. Tooltip text is "Settings". |
| 5 | Move the cursor away. | Tooltip disappears. |
| 6 | Hover over the Tips icon. | Tooltip appears to the right side. Tooltip text is "Tips". |
| 7 | Move the cursor away. | Tooltip disappears. |
| 8 | Hover over the Notifications icon (bell icon). | Tooltip appears to the right side. Tooltip text is "Notifications". |
| 9 | Move the cursor away. | Tooltip disappears. |
| 10 | Hover over the User Profile icon (avatar/name at bottom). | Tooltip appears to the right side. Tooltip text shows user name or "Profile". |
| 11 | Move the cursor away. | Tooltip disappears. |
| 12 | Using browser DevTools, inspect one of the tooltip elements and confirm the tooltip placement direction is right (e.g., MUI Tooltip placement="right" or equivalent CSS positioning). | Tooltip element CSS/attribute confirms right-side placement. |

## Expected Final State

Tooltip element CSS/attribute confirms right-side placement.

## Pass/Fail Criteria

**Pass:**
- All 5 tooltips appear to the right of their icon
- All tooltip texts match expected values
- All tooltips disappear cleanly on mouse-out

**Fail:**
- Any tooltip appears on the left, above, or below the icon
- Tooltip overlaps both the icon and the sidebar edge
- Tooltip text is incorrect or missing
- Tooltip does not appear at all on hover
