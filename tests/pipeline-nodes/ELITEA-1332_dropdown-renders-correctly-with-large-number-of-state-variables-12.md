---
id: ELITEA-1332
title: "Dropdown Renders Correctly With Large Number of State Variables (12+)"
priority: medium
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1332: Dropdown Renders Correctly With Large Number of State Variables (12+)

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the dropdown suggestion list renders correctly and remains usable when the pipeline has 12+ custom state variables — no overflow, crash, or z-index issues.

**Coverage:**
- All 14 variables (12 custom + 2 defaults) appear in the dropdown
- Dropdown is scrollable when list exceeds visible area
- No UI overflow, layout break, or z-index layering issues
- Variable selection still works correctly at scale

## Preconditions

- Logged into {{base_url}}
- Pipeline with 14 state variables total: `input`, `messages`, `var_01` through `var_12`
- LLM node with Task field set to F-String

## Test Data

State variables: `input`, `messages`, `var_01`, `var_02`, `var_03`, `var_04`, `var_05`, `var_06`, `var_07`, `var_08`, `var_09`, `var_10`, `var_11`, `var_12` (14 total)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Define 12 custom state variables (`var_01` to `var_12`) in the States sidebar in addition to the defaults `input` and `messages`. | All 14 variables listed in the States sidebar without error. |
| 2 | Open the LLM node Task field (F-String). Type `{`. | Dropdown appears and renders correctly. No overflow, layout break, or crash. List is scrollable. |
| 3 | Scroll through the full dropdown list. | All 14 variables are accessible via scrolling. No variables are cut off or missing. |
| 4 | Select `var_12` from the dropdown. | `{var_12}` is inserted into the field correctly. No other UI elements are obscured by the dropdown. |

## Expected Final State

`{var_12}` is inserted into the field correctly. No other UI elements are obscured by the dropdown.

## Pass/Fail Criteria

**Pass:**
- Dropdown renders all 14 variables with scrolling
- No overflow, crash, or z-index issues
- `{var_12}` inserts correctly

**Fail:**
- Dropdown cuts off variables, crashes, or obscures UI elements
- Selection fails with a large variable list
