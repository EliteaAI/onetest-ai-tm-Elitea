---
id: ELITEA-4780
title: "Modules switched ON are shown at the top of the Modules dropdown, above the switched OFF modules"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4780: Modules switched ON are shown at the top of the Modules dropdown, above the switched OFF modules

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that modules which are switched ON for the Agent are placed at the top of the "+ Modules" dropdown list, followed by the modules that are switched OFF.

**Coverage:**
- Ordering of enabled modules first
- Ordering after enabling modules from the middle/bottom of the list
- Ordering after Save and reload

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists with all modules switched OFF
- Browser: Chrome (latest)

## Test Data

Agent with all modules OFF; any two modules that are not at the top of the list (e.g. one in the middle and one at the bottom)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent and click "+ Modules" | Dropdown opens; all switches are OFF |
| 2 | Switch ON a module located in the middle of the list | Switch shows ON |
| 3 | Scroll down and switch ON a module located at the bottom of the list | Switch shows ON |
| 4 | Click Save | Agent is saved successfully |
| 5 | Reload the page and click "+ Modules" | The two switched-ON modules are shown at the top of the list, above all switched-OFF modules |
| 6 | Switch OFF one of the two modules, Save, reload and open "+ Modules" | Only the module still switched ON is at the top; the switched-OFF module is back among the OFF modules |
| 7 | Switch OFF the remaining module, Save, reload and open "+ Modules" | No module is pinned at the top; all modules are shown in the default order |

## Expected Final State

Switched-ON modules are always listed above switched-OFF modules.

## Pass/Fail Criteria

**Pass:** Enabled modules appear at the top of the list above disabled ones
**Fail:** An enabled module appears below a disabled module, or ordering is inconsistent after Save/reload
