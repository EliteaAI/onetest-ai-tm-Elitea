---
id: ELITEA-1333
title: "All States Disabled Including Defaults Causes No Errors and Dropdown Does Not Appear"
priority: medium
type: functional
module: pipeline-nodes
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2626]
---
# ELITEA-1333: All States Disabled Including Defaults Causes No Errors and Dropdown Does Not Appear

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when all state variables — including the default `input` and `messages` — are disabled, typing `{` in an F-String field does not trigger a dropdown, and the pipeline does not crash or throw unhandled errors.

**Coverage:**
- Disabling all states (including defaults) via the States sidebar toggle
- No dropdown appears in F-String field when no states are active
- Node saves without error in this configuration
- Pipeline runs (or fails gracefully) without a crash

## Preconditions

- Logged into {{base_url}}
- Pipeline with default state variables `input` and `messages`
- LLM node with Task field available

## Test Data

State variables to disable: `input`, `messages`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the States sidebar. Toggle off `input`. Toggle off `messages`. Confirm no state variables are active. | Both default states are disabled. States sidebar shows no active variables. |
| 2 | Open the LLM node. Set the Task field type to F-String. Click inside the field and type `{`. | No dropdown appears — there are no state variables to suggest. |
| 3 | Type some plain text (e.g., `Analyze the data`). Save the node and save the pipeline. | Node and pipeline save without error despite no active state variables. |
| 4 | Run the pipeline via Chat. | Pipeline executes or fails gracefully with a clear message. No unhandled crash or JS error occurs related to the disabled states. |

## Expected Final State

Pipeline executes or fails gracefully with a clear message. No unhandled crash or JS error occurs related to the disabled states.

## Pass/Fail Criteria

**Pass:**
- No dropdown appears when all states are disabled
- Node and pipeline save without error
- No crash occurs on run

**Fail:**
- Dropdown appears empty or throws an error when states are disabled
- Pipeline or UI crashes when all states are toggled off
