---
id: ELITEA-1344
title: "Bug #3932: Input Field Clears When Type Changes Away From F-String"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3932, ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1344: Bug #3932: Input Field Clears When Type Changes Away From F-String

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when the Input field type is changed between F-String, Fixed, and Variable, previously entered values do not persist (regression test for Bug #3932).

**Coverage:**
- Input field cleared on type change from F-String → Fixed
- Input field cleared on type change from Fixed → Variable
- No stale values cross-contaminating between type changes

## Preconditions

- Pipeline editor open with HITL node on canvas; configuration panel open
- Focus on the Input field section

## Test Data

F-String value: Hello {{state.input}}; Fixed value: Static message

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set the Input type to F-String | F-String type selected; text input field available |
| 2 | Enter 'Hello {{state.input}}' in the Input field | Text appears in the field |
| 3 | Change the Input type to Fixed | The Input field clears — the F-String value 'Hello {{state.input}}' is NOT present; field is empty or shows Fixed placeholder |
| 4 | Enter 'Static message' in the Fixed Input field | Text appears correctly |
| 5 | Change the type from Fixed to Variable | The Fixed value 'Static message' is NOT present; field clears |
| 6 | Change type back to F-String and verify the field | Field is empty — no residual value from any previous type |

## Expected Final State

Field is empty — no residual value from any previous type

## Pass/Fail Criteria

**Pass:**
- Input field is fully cleared each time the type changes
- Zero stale values carry over between type changes

**Fail:**
- Previously entered value persists after a type change (Bug #3932 regression)
- Any cross-type value contamination
