---
id: ELITEA-4783
title: "Switching modules on and off activates Save and Discard, Save keeps the changes after reload, and Discard restores the previous states"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, persistence, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4783: Switching modules on and off activates Save and Discard, Save keeps the changes after reload, and Discard restores the previous states

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changing module switches in the "+ Modules" dropdown marks the Agent as changed (Save and Discard become active), that saved module states persist after a page reload, and that Discard reverts unsaved module changes.

**Coverage:**
- Save / Discard activation on module change
- Persistence after Save and reload
- Discard reverts unsaved changes (dropdown closed and open)

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists with at least one module ON and at least two modules OFF
- No unsaved changes on the Agent (Save and Discard are disabled)
- Browser: Chrome (latest)

## Test Data

Any existing editable Agent; modules chosen from the top and the bottom of the list

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent, click "+ Modules" and note the state of every module | Initial states are recorded; Save and Discard are disabled |
| 2 | Switch ON one module that is OFF | Switch shows ON; Save and Discard become active |
| 3 | Scroll down and switch ON a module at the bottom of the list | Switch shows ON |
| 4 | Switch OFF a module that was ON | Switch shows OFF |
| 5 | Click Save | Agent is saved; success notification is shown; Save and Discard become disabled |
| 6 | Reload the page and click "+ Modules" | The three changed modules show the saved states; all other modules are unchanged |
| 7 | Switch two modules to the opposite state and close the dropdown | Save and Discard are active |
| 8 | Click Discard | Changes are discarded; Save and Discard become disabled |
| 9 | Click "+ Modules" | Both modules show the states saved in step 5 |
| 10 | Switch one module, keep the dropdown open and click Discard | Change is discarded; the module shows its saved state |

## Expected Final State

Saved module states persist after reload; Discard restores the last saved states.

## Pass/Fail Criteria

**Pass:** Save/Discard activate on module change, saved states persist after reload, Discard reverts unsaved changes
**Fail:** Save/Discard do not activate, states are lost or wrong after reload, or Discard does not revert module changes
