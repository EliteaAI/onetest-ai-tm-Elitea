---
id: ELITEA-4897
title: "Verify bottom row is fixed 52 px with divider and Support Assistant in its cell"
priority: critical
type: functional
module: new-sidebar
status: ready
execution_type: manual
tags: [r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4897: Verify bottom row is fixed 52 px with divider and Support Assistant in its cell


## Preconditions

- User is logged in to `{{base_url}}`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Sidebar state | Expanded; Collapsed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` with the sidebar expanded | The bottom row is visible at the bottom of the sidebar |
| 2 | Inspect the bottom row in DevTools | The row height is **52 px** and there is a divider line at its top |
| 3 | Check the Support Assistant button position | It sits inside the right cell of the bottom row, centred: about 11 px below the divider and 12 px above the window edge. It is not floating in a window corner |
| 4 | Collapse the sidebar with the existing control | The sidebar collapses to the compact rail |
| 5 | Repeat steps 2–3 in the collapsed state | The bottom area is 52 px with a divider, and the Support Assistant is centred in its cell |

## Expected Final State

The bottom row is fixed and holds the Support Assistant in both sidebar states.

## Pass/Fail Criteria

**Pass:**
- The row is 52 px with a top divider in both states
- The Support Assistant is placed inside the row cell

**Fail:**
- The row height is different or the divider is missing
- The Support Assistant floats in a window corner or overlaps other controls
