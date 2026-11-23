---
id: ELITEA-4786
title: "Modules dropdown stays open while several modules are switched one after another"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4786: Modules dropdown stays open while several modules are switched one after another

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "+ Modules" dropdown does not close after a module is switched, so the user can configure several modules in a row without reopening it.

**Coverage:**
- Dropdown remains open after each switch
- Switching modules at the top and bottom of the list
- Quick repeated switching of the same module

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists
- Browser: Chrome (latest)

## Test Data

Any existing editable Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent and click "+ Modules" | Dropdown opens |
| 2 | Switch the first module in the list | Switch changes state; dropdown stays open |
| 3 | Switch a second module | Switch changes state; dropdown stays open |
| 4 | Scroll down and switch a module at the bottom of the list | Switch changes state; dropdown stays open and scroll position is kept |
| 5 | Switch a fourth module | Switch changes state; dropdown stays open |
| 6 | Switch the same module ON and OFF quickly three times | Switch follows every click; final state matches the last click; dropdown stays open |
| 7 | Press Escape | Dropdown closes |
| 8 | Click "+ Modules" again | All switches show the states set in steps 2–6 |

## Expected Final State

All switched modules keep their new states and the dropdown closed only on Escape.

## Pass/Fail Criteria

**Pass:** Dropdown stays open during all switch actions and keeps the switched states
**Fail:** Dropdown closes after a switch, loses scroll position, or a switch state is lost
