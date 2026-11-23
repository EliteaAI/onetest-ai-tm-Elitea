---
id: ELITEA-4778
title: "Agent Tools row shows + Modules after + Pipeline, old MODULES grid is removed, and the button opens a searchable module list"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4778: Agent Tools row shows + Modules after + Pipeline, old MODULES grid is removed, and the button opens a searchable module list

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Agent detail view shows the new "+ Modules" button in the TOOLS row right after "+ Pipeline", that the old expanded MODULES grid (with Show all / Show less) is no longer displayed, and that clicking "+ Modules" opens a dropdown with a search field and the module list.

**Coverage:**
- Button presence and position in the TOOLS row
- Removal of the old MODULES grid
- Dropdown opens with "Search modules..." field and module list

## Preconditions

- Logged in to {{base_url}}
- At least one editable Agent exists in the project
- Browser: Chrome (latest)

## Test Data

Any existing editable Agent; a new unsaved Agent (Create Agent page)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agents and open an existing Agent | Agent detail view is displayed |
| 2 | Locate the TOOLS section | TOOLS row shows buttons in order: + Toolkit, + MCP, + Agent, + Pipeline, + Modules |
| 3 | Look below the TOOLS row | No MODULES heading, no module switch cards and no Show all / Show less control are displayed |
| 4 | Click "+ Modules" | A dropdown opens below the button |
| 5 | Observe the dropdown content | A "Search modules..." field is displayed at the top, followed by the list of modules |
| 6 | Click outside the dropdown | Dropdown closes |
| 7 | Open Create Agent page (+ Agent in the sidebar) and repeat steps 2–5 | Same layout and behaviour as for the existing Agent |

## Expected Final State

The "+ Modules" button is the last button in the TOOLS row and opens a searchable module dropdown; the old MODULES grid is not shown.

## Pass/Fail Criteria

**Pass:** "+ Modules" is displayed after "+ Pipeline", the old MODULES grid is absent, and the dropdown opens with a search field and module list
**Fail:** "+ Modules" is missing or misplaced, the old MODULES grid is still shown, or the dropdown does not open / lacks the search field or list
