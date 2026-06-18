---
id: ELITEA-1334
title: "F-String Dropdown Not Triggered for Fixed or Variable Field Types [Parametrized]"
priority: high
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1334: F-String Dropdown Not Triggered for Fixed or Variable Field Types [Parametrized]

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that the `{` keystroke does NOT trigger the F-String state variable dropdown when a node field is set to Fixed or Variable type — this behavior must be exclusive to F-String type fields.

**Coverage:**
- `{` in Fixed-type field is typed literally — no dropdown appears
- Variable-type field uses its own dedicated picker — no `{`-triggered dropdown
- Behavior verified for LLM and Toolkit nodes

## Preconditions

- Logged into {{base_url}}
- Pipeline with LLM node and Toolkit node configured

## Test Data

Field types to test: Fixed, Variable. Nodes: LLM (Task), Toolkit (Input Mapping parameter).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the LLM node. Set the Task field type to **Fixed**. Click inside the field and type `{`. | No F-String dropdown appears. The `{` character is typed literally into the field. |
| 2 | Set the Task field type to **Variable**. Interact with the field. | A dedicated state variable picker/select control appears (appropriate for Variable type). No `{`-triggered inline dropdown appears. |
| 3 | Open the Toolkit node. Set an Input Mapping parameter type to **Fixed**. Click inside the value field and type `{`. | No F-String dropdown appears. Character is typed literally. |
| 4 | Set the same Toolkit Input Mapping parameter type to **Variable**. Interact with the field. | Dedicated variable picker appears. No `{`-triggered inline dropdown. |

## Expected Final State

Dedicated variable picker appears. No `{`-triggered inline dropdown.

## Pass/Fail Criteria

**Pass:**
- No F-String dropdown appears for Fixed or Variable field types in any tested node
- Variable type uses its own correct picker control

**Fail:**
- F-String dropdown appears when field type is Fixed or Variable
