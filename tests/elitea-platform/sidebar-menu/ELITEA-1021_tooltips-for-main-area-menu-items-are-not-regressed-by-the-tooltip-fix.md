---
id: ELITEA-1021
title: "Tooltips for Main-Area Menu Items Are Not Regressed by the Tooltip Fix"
priority: high
type: functional
module: sidebar-menu
status: ready
execution_type: manual
tags: [nfr:usability, r-2.0.1, 3846]
requirements: [ProjectAlita/projectalita.github.io#3846]
---
# ELITEA-1021: Tooltips for Main-Area Menu Items Are Not Regressed by the Tooltip Fix

**Module:** Sidebar Menu · **Priority:** High · **Type:** Functional

**Objective:** Verify that the tooltip position fix for bottom-bar items did not inadvertently change the tooltip positioning for the main navigation area items.

**Coverage:**
- Chat tooltip position is correct (right side)
- Agents tooltip position is correct
- Pipelines tooltip position is correct
- Credentials tooltip position is correct
- Toolkits tooltip position is correct
- MCPs tooltip position is correct
- Artifacts tooltip position is correct

## Preconditions

- User is logged in to ELITEA
- Sidebar is in collapsed (icon-only) mode

## Test Data

- Main sidebar items to verify: Chat, Agents, Pipelines, Credentials, Toolkits, MCPs, Artifacts

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Collapse the sidebar to icon-only mode. | Sidebar shows icons only. |
| 2 | Hover over Chat icon. | Tooltip appears to the right side. Tooltip text is "Chat". |
| 3 | Hover over Agents icon. | Tooltip appears to the right side. Tooltip text is "Agents". |
| 4 | Hover over Pipelines icon. | Tooltip appears to the right side. Tooltip text is "Pipelines". |
| 5 | Hover over Credentials icon. | Tooltip appears to the right side. Tooltip text is "Credentials". |
| 6 | Hover over Toolkits icon. | Tooltip appears to the right side. Tooltip text is "Toolkits". |
| 7 | Hover over MCPs icon. | Tooltip appears to the right side. Tooltip text is "MCPs". |
| 8 | Hover over Artifacts icon. | Tooltip appears to the right side. Tooltip text is "Artifacts". |
| 9 | For each item, confirm the tooltip disappears cleanly when the cursor moves away. | All tooltips disappear correctly. |

## Expected Final State

All tooltips disappear correctly.

## Pass/Fail Criteria

**Pass:**
- All 7 main-area tooltips appear on the right side of their icon
- All tooltip texts are correct
- Tooltips disappear on mouse-out

**Fail:**
- Any main-area tooltip is repositioned to a wrong side (top/bottom/left)
- Any tooltip is missing or shows incorrect text
- Any tooltip fails to disappear
