---
id: ELITEA-4925
title: "Sidebar structure, 288 px width and fixed 52 px bottom row with Support Assistant"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7562]
---
# ELITEA-4925: Sidebar structure, 288 px width and fixed 52 px bottom row with Support Assistant

## Preconditions

- User is logged in to `{{base_url}}`
- User has a personal project with at least one chat
- Sidebar is expanded

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Viewport | 1366 × 768 |
| Expected order | Logo + bell → project selector → + New chat → Artifacts → Explore → Chats history → bottom row |
| Bottom row | Settings, Help (?), Support Assistant |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `{{base_url}}/app/` at 1366 × 768 | The chat page opens with the sidebar expanded |
| 2 | Check the sidebar from top to bottom | The areas appear in the expected order from the Test Data |
| 3 | Look for standalone Chats, Catalog, Agents, Pipelines, Skills, Toolkits, MCPs, Applications and Credentials menu items | None of them appear as separate sidebar items |
| 4 | Inspect the sidebar container in DevTools | The computed width is **288 px** |
| 5 | Inspect the bottom row | It is **52 px** high with a divider at its top, and holds Settings, Help (?) and Support Assistant from left to right |
| 6 | Check the Support Assistant button | It sits centred in the right cell of the bottom row, not floating in a window corner |
| 7 | Collapse the sidebar with the existing control and check the bottom area | The bottom area is still 52 px with a divider, and the Support Assistant is centred in its cell |
| 8 | Expand the sidebar again | The width returns to 288 px and the order from step 2 is unchanged |

## Expected Final State

The expanded sidebar has the new structure and width, and the bottom row is fixed with the Support Assistant inside it in both states.

## Pass/Fail Criteria

**Pass:**
- Order, width and bottom row match the Test Data in both sidebar states
- No removed menu item is visible

**Fail:**
- Any area is missing or out of order, or a removed item is still shown
- Width is not 288 px, or the bottom row height or divider is wrong
- The Support Assistant floats in a window corner or overlaps other controls

## Notes

**Source functional tests:** ELITEA-4895, ELITEA-4896, ELITEA-4897
**Regression rationale:** One pass over the sidebar shell catches layout regressions to every entry point at once.
**Selected checkpoints:** Area order; removed items gone; 288 px width; 52 px bottom row with divider; Support Assistant in its cell in both states.
