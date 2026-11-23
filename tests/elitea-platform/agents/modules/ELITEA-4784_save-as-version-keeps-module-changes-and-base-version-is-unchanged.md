---
id: ELITEA-4784
title: "Save As Version keeps module changes on the new version and leaves the base version unchanged"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:agents, nfr:ui, modules, versioning, 7380]
requirements: [EliteaAI/elitea_issues#7380]
---
# ELITEA-4784: Save As Version keeps module changes on the new version and leaves the base version unchanged

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that module changes made in the "+ Modules" dropdown are stored on a new version created with Save As Version, while the base version keeps its original module states.

**Coverage:**
- Module state on the new version
- Base version module state unchanged
- Switching between versions

## Preconditions

- Logged in to {{base_url}}
- An editable Agent exists on its base version
- Browser: Chrome (latest)

## Test Data

Version name: "modules-v2"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent (base version), click "+ Modules" and note every module state | Base version states are recorded |
| 2 | Switch two modules to the opposite state | Switches change; Save As Version is available |
| 3 | Click Save As Version, enter "modules-v2" and confirm | New version "modules-v2" is created and opened |
| 4 | Click "+ Modules" | The two modules show the changed states; other modules match the base version |
| 5 | Switch the version selector to base | Base version opens |
| 6 | Click "+ Modules" | All modules show the states recorded in step 1 |
| 7 | Switch to "modules-v2" and back to base again | Each version shows its own module states every time |

## Expected Final State

The new version has the changed module states; the base version is unchanged.

## Pass/Fail Criteria

**Pass:** New version stores the module changes and base version keeps its original states
**Fail:** New version is missing the changes, or base version module states are modified
