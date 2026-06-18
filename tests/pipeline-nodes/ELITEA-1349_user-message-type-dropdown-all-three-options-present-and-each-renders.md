---
id: ELITEA-1349
title: "USER MESSAGE Type Dropdown: All Three Options Present and Each Renders the Correct Fields"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1349: USER MESSAGE Type Dropdown: All Three Options Present and Each Renders the Correct Fields

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that the USER MESSAGE type dropdown offers exactly three options (F-String, Variable, Fixed) and that each renders the appropriate input control.

**Coverage:**
- Dropdown lists all three type options exactly
- F-String type shows a text area with template support
- Variable type shows a state variable picker dropdown
- Fixed type shows a plain text input

## Preconditions

- Pipeline editor open; HITL node on canvas; configuration panel open
- Focus on the USER MESSAGE section

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the USER MESSAGE type dropdown | Dropdown opens showing exactly: F-String, Variable, Fixed |
| 2 | Select F-String | A multi-line text area appears supporting {{variable}} syntax |
| 3 | Select Variable | A dropdown variable picker appears listing pipeline state variables |
| 4 | Select Fixed | A plain text input field appears with no variable syntax indicators |
| 5 | Cycle through all three types in sequence | Each transition is smooth; correct field renders for each type; no UI glitches |

## Expected Final State

Each transition is smooth; correct field renders for each type; no UI glitches

## Pass/Fail Criteria

**Pass:**
- Exactly three options in dropdown
- Each type renders the correct input control

**Fail:**
- Any option missing from dropdown
- Wrong control rendered for a given type
- UI breaks during type switching
