---
id: ELITEA-4782
title: "Arrow Down and Arrow Up move through every module in the Modules dropdown and scroll the focused module into view"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, keyboard, a11y, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4782: Arrow Down and Arrow Up move through every module in the Modules dropdown and scroll the focused module into view

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that keyboard navigation with Arrow Down / Arrow Up reaches every module in the "+ Modules" dropdown and that the list scrolls so the focused module is always fully visible.

**Coverage:**
- Arrow Down navigation to the last module
- Arrow Up navigation back to the first module
- Focused module scrolled into view
- Visible focus indicator

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists
- More modules are available than fit in the dropdown without scrolling
- Browser: Chrome (latest)

## Test Data

Any existing editable Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent and click "+ Modules" | Dropdown opens with the search field focused or available |
| 2 | Press Arrow Down | Focus moves from the search field to the first module; focus indicator is visible |
| 3 | Keep pressing Arrow Down one module at a time | Focus moves to the next module each time; when focus reaches a module below the visible area, the list scrolls and the focused module is fully visible |
| 4 | Continue until the last module | Last module is focused and fully visible at the bottom of the dropdown |
| 5 | Press Arrow Down once more | Focus stays on the last module or wraps to the first module without errors; the focused module is visible |
| 6 | Press Arrow Up repeatedly until the first module | Focus moves up one module at a time; the list scrolls up so the focused module is always fully visible |
| 7 | Check that no module was skipped during steps 3–6 | Every module in the list received focus |

## Expected Final State

All modules are reachable with Arrow keys and the focused module is always visible.

## Pass/Fail Criteria

**Pass:** Arrow Down/Up reach every module and the list scrolls the focused module into view
**Fail:** Any module is skipped or unreachable, focus is invisible, or the focused module stays out of view / clipped
