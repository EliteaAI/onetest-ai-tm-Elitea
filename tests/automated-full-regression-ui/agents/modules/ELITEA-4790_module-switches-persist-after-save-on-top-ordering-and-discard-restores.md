---
id: ELITEA-4790
title: "Module switches are kept after Save and reload with switched-ON modules on top, and Discard restores saved states"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents, nfr:ui, modules, persistence, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4790: Module switches are kept after Save and reload with switched-ON modules on top, and Discard restores saved states

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that several modules can be switched in a row without the dropdown closing, that Save and Discard become active, that saved states persist after reload with switched-ON modules shown at the top of the list, and that Discard reverts unsaved module changes.

## Preconditions

- Logged in to `{{base_url}}`
- An editable Agent exists with all modules switched OFF and no unsaved changes
- Browser: Chrome (latest)

## Test Data

| Field | Value |
|---|---|
| Agent | Editable Agent with all modules OFF |
| Module A | A module in the middle of the list |
| Module B | The last module in the list |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent and click "+ Modules" | Dropdown opens; all switches are OFF; Save and Discard are disabled |
| 2 | Switch Module A ON | Switch shows ON; dropdown stays open; Save and Discard become active |
| 3 | Scroll down and switch Module B ON | Switch shows ON; dropdown stays open |
| 4 | Press Escape and click Save | Agent is saved; Save and Discard become disabled |
| 5 | Reload the page and click "+ Modules" | Module A and Module B are ON and shown at the top of the list, above all switched-OFF modules |
| 6 | Switch Module A OFF and close the dropdown | Save and Discard are active |
| 7 | Click Discard | Changes are discarded; Save and Discard become disabled |
| 8 | Click "+ Modules" | Module A and Module B are still ON at the top of the list |
| 9 | Cleanup: switch Module A and Module B OFF and click Save | All modules are OFF |

## Expected Final State

Saved module states persist after reload, switched-ON modules are on top, and Discard restores the saved states.

## Pass/Fail Criteria

**Pass:**
- Dropdown stays open while switching; saved states persist after reload with ON modules on top; Discard reverts unsaved changes

**Fail:**
- Dropdown closes after a switch, states are lost after reload, ON modules are not on top, or Discard does not revert

## Notes

**Source functional tests:** ELITEA-4783, ELITEA-4780, ELITEA-4786, ELITEA-4785
**Regression rationale:** Persistence is the core purpose of the dropdown; losing module configuration silently changes agent behaviour.
**Selected checkpoints:** Dropdown stays open; Save/Discard activation; persistence after reload; ON-first ordering; correct states shown on load; Discard restore.
