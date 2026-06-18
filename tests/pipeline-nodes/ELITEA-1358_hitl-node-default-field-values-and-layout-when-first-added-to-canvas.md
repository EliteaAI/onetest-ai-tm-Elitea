---
id: ELITEA-1358
title: "HITL Node Default Field Values and Layout When First Added to Canvas"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1358: HITL Node Default Field Values and Layout When First Added to Canvas

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a freshly added HITL node has sensible default values in all fields, and the configuration panel layout is correct.

**Coverage:**
- Default values for Input type, USER MESSAGE type, EDIT STATE KEY
- All four sections visible and correctly labeled
- Clean, non-broken layout

## Preconditions

- Pipeline editor open (new or existing pipeline)

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Drag a new HITL node onto the canvas for the first time | HITL node appears on canvas |
| 2 | Click the HITL node to open the configuration panel | Configuration panel opens |
| 3 | Inspect all default values without making any changes | All fields have sensible defaults (types preset, values empty or placeholder); no unexpected pre-filled data |
| 4 | Verify layout: sections Input, USER MESSAGE, ROUTER MAPPING, EDIT STATE KEY are all visible | Layout is clean; sections correctly labeled; no overlapping elements or truncated labels |

## Expected Final State

Layout is clean; sections correctly labeled; no overlapping elements or truncated labels

## Pass/Fail Criteria

**Pass:**
- Defaults are sensible and predictable
- All sections visible and cleanly laid out

**Fail:**
- Unexpected pre-filled values on a fresh node
- Missing sections or broken layout
