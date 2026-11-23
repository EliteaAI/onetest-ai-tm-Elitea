---
id: ELITEA-4779
title: "Modules dropdown lists every available module exactly once, each row with icon, name, info icon and on/off switch"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4779: Modules dropdown lists every available module exactly once, each row with icon, name, info icon and on/off switch

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "+ Modules" dropdown contains every module available on the environment, with no module missing, duplicated, hidden or cut off, and that each row shows the module icon, name, info (i) icon and an on/off switch.

**Coverage:**
- Completeness of the module list (compared against the environment's own module list)
- No duplicates
- Row structure (icon, name, info icon, switch)

> Note: The number and names of modules can change between releases and environments. Do not compare against a fixed list — build the reference list from the environment under test.

## Preconditions

- Logged in to {{base_url}}
- At least one editable Agent exists
- Reference list of available modules is known for the environment (e.g. from Settings > General > Default Modules for Agents)
- Browser: Chrome (latest)

## Test Data

Any existing editable Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Settings > General > Default Modules and note all modules available for Agents | Reference list of modules is recorded |
| 2 | Open an existing Agent and click "+ Modules" | Modules dropdown opens |
| 3 | Note the modules visible without scrolling | Visible modules are recorded |
| 4 | Scroll the list to the very bottom and note the remaining modules | All remaining modules are recorded |
| 5 | Compare the combined list with the reference list | Every module from the reference list is present in the dropdown; no extra or missing modules |
| 6 | Check the list for repeated entries | Each module appears exactly once |
| 7 | Inspect each row | Each row shows a module icon, module name, info (i) icon and an on/off switch; no row is cut off or overlapped |
| 8 | Repeat steps 2–7 on the Create Agent page (new unsaved Agent) | Same complete list and row structure |

## Expected Final State

The dropdown contains all available modules exactly once, each with icon, name, info icon and switch.

## Pass/Fail Criteria

**Pass:** All available modules are listed once with complete row elements
**Fail:** Any module is missing, duplicated, hidden, cut off, or a row lacks its icon, name, info icon or switch
