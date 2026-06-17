---
id: ELITEA-0845
title: "Verify pipeline state creation applies default values based on field type"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0845: Verify pipeline state creation applies default values based on field type

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** When creating pipeline states, the system does not apply default values based on the selected field type. For example, an integer field should default to 0, an array field should default to an empty array [], and a string field should default to an empty string. This test verifies that default values are automatically set based on the state field type.

## Preconditions

User logged into Elitea stage.elitea.ai
User can create and configure pipelines with state variables

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new pipeline or open an existing one in the pipeline editor | Pipeline editor loads with Flow view active |
| 2 | Add a State modifier node to the pipeline | State modifier node appears on the canvas |
| 3 | Create a new state variable with type 'String' and do not manually set a default value | String state variable is created. Default value should automatically be set to empty string '' |
| 4 | Create a new state variable with type 'Integer' and do not manually set a default value | Integer state variable is created. Default value should automatically be set to 0 |
| 5 | Create a new state variable with type 'Array' and do not manually set a default value | Array state variable is created. Default value should automatically be set to empty array [] |
| 6 | Create a new state variable with type 'Boolean' and do not manually set a default value | Boolean state variable is created. Default value should automatically be set to false |
| 7 | Switch to YAML editor view and inspect the state variable definitions | YAML shows each state variable with its correct type-appropriate default value (string: '', integer: 0, array: [], boolean: false) |
| 8 | Save the pipeline and reload the page. Verify default values persist correctly | After save and reload, all state variables retain their type-appropriate default values |
| 9 | Execute the pipeline and verify state variables start with correct default values in run details | Run details show state variables initialized with their type-appropriate defaults at the start of execution |

## Expected Final State

Run details show state variables initialized with their type-appropriate defaults at the start of execution

## Pass/Fail Criteria

PASS: All state variable types automatically get correct default values upon creation without manual intervention
FAIL: State variables are created without default values, or default values don't match the field type (e.g., integer defaults to null instead of 0)
