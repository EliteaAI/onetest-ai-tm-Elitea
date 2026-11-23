---
id: ELITEA-4781
title: "Modules dropdown list scrolls to both ends with mouse wheel and scrollbar, first and last modules are fully visible, page behind does not scroll"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, scroll, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4781: Modules dropdown list scrolls to both ends with mouse wheel and scrollbar, first and last modules are fully visible, page behind does not scroll

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "+ Modules" dropdown list can be scrolled down to the last module and back up to the first module using the mouse wheel and the scrollbar, that the first and last modules are fully visible (not clipped by the dropdown edges), and that scrolling the list does not scroll the Agent page behind it.

**Coverage:**
- Mouse wheel scrolling
- Scrollbar dragging
- Last module fully visible at the bottom
- First module fully visible at the top
- Scroll isolation from the page

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists
- More modules are available than fit in the dropdown without scrolling
- Browser: Chrome (latest), window 1920x1080, zoom 100%

## Test Data

Any existing editable Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent and click "+ Modules" | Dropdown opens; first modules are visible, the list is scrollable |
| 2 | Scroll down with the mouse wheel until the list stops | List scrolls smoothly to the end |
| 3 | Check the last module in the list | Last module row (icon, name, info icon, switch) is fully visible and not cut off by the bottom edge of the dropdown |
| 4 | Observe the Agent page behind the dropdown during step 2 | The page behind does not scroll |
| 5 | Scroll up with the mouse wheel until the list stops | List scrolls back to the top |
| 6 | Check the first module in the list | First module row is fully visible directly below the search field, not hidden under it |
| 7 | Drag the dropdown scrollbar (if displayed) to the bottom | List shows the last module fully visible |
| 8 | Drag the scrollbar back to the top | List shows the first module fully visible |
| 9 | Confirm the dropdown is still open | Dropdown remains open after scrolling and scrollbar interaction |

## Expected Final State

The full module list is reachable by scrolling; first and last modules are fully visible; page behind is not scrolled.

## Pass/Fail Criteria

**Pass:** List scrolls to both ends with wheel and scrollbar, first and last modules are fully visible, page does not scroll
**Fail:** List does not scroll, any module cannot be reached, first/last module is clipped, or the page behind scrolls
