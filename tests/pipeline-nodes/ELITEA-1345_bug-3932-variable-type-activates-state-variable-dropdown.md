---
id: ELITEA-1345
title: "Bug #3932: Variable Type Activates State Variable Dropdown"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3932, ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1345: Bug #3932: Variable Type Activates State Variable Dropdown

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting "Variable" as the Input type renders an active, functional state variable dropdown (regression test for Bug #3932 — previously the dropdown did not activate).

**Coverage:**
- Variable type renders a dropdown (not a disabled text field)
- Dropdown opens and lists available state variables
- Variable selection persists correctly
- Dropdown reactivates on re-selecting Variable type

## Preconditions

- Pipeline editor open with HITL node; configuration panel open
- Pipeline has at least one state variable defined (for the dropdown to be non-empty)

## Test Data

At least one pipeline state variable (e.g., state.input)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Input type to F-String; confirm the text input field is shown | Standard text input visible |
| 2 | Change the Input type to Variable | A dropdown control appears (not a plain text input); dropdown is active and enabled |
| 3 | Click on the dropdown | Dropdown expands; lists available pipeline state variables |
| 4 | Select a state variable (e.g., state.input) | Selected variable name is shown in the field; no errors |
| 5 | Change type to F-String, then back to Variable | Variable dropdown re-appears in an active, clickable state every time |

## Expected Final State

Variable dropdown re-appears in an active, clickable state every time

## Pass/Fail Criteria

**Pass:**
- Variable type always shows an active, clickable dropdown
- Dropdown lists pipeline state variables
- Dropdown re-activates on repeat type changes

**Fail:**
- Variable type shows a plain disabled text field instead of a dropdown (Bug #3932 regression)
- Dropdown does not open
- No variables listed in the dropdown
