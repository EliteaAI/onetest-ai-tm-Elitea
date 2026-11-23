---
id: ELITEA-4789
title: "Modules dropdown opens from the Tools row, lists every available module and scrolls to a fully visible last module"
priority: critical
type: functional
module: agents
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.agents.test_agent_modules_dropdown.test_modules_dropdown_lists_all_modules_and_scrolls_to_last
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/5a48ef4319aa00d01b5008245414fc3911be4b7b
tags: [automated:UI:regression, feat:agents, nfr:ui, modules, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4789: Modules dropdown opens from the Tools row, lists every available module and scrolls to a fully visible last module

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "+ Modules" button is shown after "+ Pipeline" in the Agent TOOLS row instead of the old MODULES grid, that it opens a searchable dropdown listing every available module exactly once, and that the list scrolls to the end with the last module fully visible.

> The number and names of modules can change. Build the reference list from the environment under test, not from a fixed list.

## Preconditions

- Logged in to `{{base_url}}`
- An editable Agent exists
- More modules are available than fit in the dropdown without scrolling
- Reference list of available Agent modules is known (Settings > General > Default Modules)
- Browser: Chrome (latest), window 1920x1080, zoom 100%

## Test Data

| Field | Value |
|---|---|
| Agent | Any existing editable Agent |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent and locate the TOOLS section | Buttons in order: + Toolkit, + MCP, + Agent, + Pipeline, + Modules |
| 2 | Look below the TOOLS row | No MODULES grid and no Show all / Show less control is displayed |
| 3 | Click "+ Modules" | Dropdown opens with a "Search modules..." field and the module list |
| 4 | Check a row in the list | Row shows a module icon, name, info (i) icon and an on/off switch |
| 5 | Scroll the list down with the mouse wheel until it stops | List scrolls to the end; the page behind does not scroll |
| 6 | Check the last module in the list | Last module row is fully visible, not cut off by the bottom edge of the dropdown |
| 7 | Compare all modules seen in the list with the reference list | Every available module is present exactly once; none is missing or duplicated |
| 8 | Scroll back to the top | First module is fully visible below the search field |
| 9 | Press Escape | Dropdown closes |

## Expected Final State

The dropdown lists all available modules and every module, including the last one, is reachable and fully visible.

## Pass/Fail Criteria

**Pass:**
- + Modules is displayed after + Pipeline and the old grid is gone
- All available modules are listed once and the last module is fully visible after scrolling

**Fail:**
- + Modules is missing or misplaced, the old grid is shown, a module is missing/duplicated, or the list does not scroll / clips the last module

## Notes

**Source functional tests:** ELITEA-4778, ELITEA-4779, ELITEA-4781
**Regression rationale:** Protects the main entry point to agent modules; if the dropdown breaks or clips items, users cannot configure modules.
**Selected checkpoints:** Button position; old grid removed; dropdown opens with search; complete list; scroll to fully visible last module; page does not scroll.
