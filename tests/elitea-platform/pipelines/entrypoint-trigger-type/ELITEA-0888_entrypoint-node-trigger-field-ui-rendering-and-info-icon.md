---
id: ELITEA-0888
title: "Entrypoint Node — Trigger Field UI Rendering and Info Icon"
priority: medium
type: functional
module: entrypoint-trigger-type
status: ready
execution_type: manual
tags: [pipeline, R-2.0.3, trigger]
requirements: [#4827]
---
# ELITEA-0888: Entrypoint Node — Trigger Field UI Rendering and Info Icon

**Module:** Entrypoint Trigger Type · **Priority:** Medium · **Type:** Functional

**Objective:** Verifies that the Trigger label includes a visible info icon on the Entrypoint node card, and that the trigger field is rendered at the top of the node card above other configuration fields.

## Preconditions

User is logged in with pipeline edit permissions
A pipeline with an Entrypoint node exists

## Test Data

Pipeline with an Entrypoint node that also has other config fields (e.g., variables)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline with an Entrypoint node in edit mode | Pipeline canvas loads |
| 2 | Click the Entrypoint node to open its configuration panel | Node config panel is displayed |
| 3 | Observe the position of the Trigger field relative to other config fields on the node card | The Trigger field/label appears at the top of the Entrypoint node configuration, above all other node-specific configuration fields |
| 4 | Observe the Trigger label for any accompanying icon | A visible info icon is present alongside the 'Trigger' label on the node card |

## Expected Final State

A visible info icon is present alongside the 'Trigger' label on the node card

## Pass/Fail Criteria

PASS: Info icon visible next to the Trigger label; Trigger field is topmost in the node config panel
FAIL: No info icon present; Trigger field is below other config fields
