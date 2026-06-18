---
id: ELITEA-1340
title: "HITL Node Available in Pipeline Node Palette and Renders Correctly"
priority: critical
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1340: HITL Node Available in Pipeline Node Palette and Renders Correctly

**Module:** Pipeline Nodes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the HITL node appears in the pipeline node palette, can be added to the canvas, and renders all expected visual elements and configuration fields.

**Coverage:**
- Node palette visibility with headphone icon
- Canvas rendering with three output handles (Approve / Edit / Reject)
- Configuration panel sections: Input, USER MESSAGE, ROUTER MAPPING, EDIT STATE KEY

## Preconditions

- Logged in to ELITEA with pipeline creation/edit permissions
- Pipeline editor open in Flow view (create new or open existing pipeline)
- Browser: Chrome (latest)

## Test Data

Any project with a pipeline editor accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline editor and inspect the node sidebar/palette | A "HITL" node type is visible in the palette, identifiable by a headphone icon |
| 2 | Drag the HITL node from the palette onto the pipeline canvas | Node appears on canvas with a headphone icon and three labeled output handles: Approve, Edit, Reject |
| 3 | Click the HITL node to open its configuration panel | Configuration panel opens showing: Input field (with type dropdown), USER MESSAGE section, ROUTER MAPPING section, and EDIT STATE KEY field |
| 4 | Verify node visual elements: headphone icon, node label "HITL", output handle labels | All labels are correct; headphone icon is displayed; no visual glitches |

## Expected Final State

All labels are correct; headphone icon is displayed; no visual glitches

## Pass/Fail Criteria

**Pass:**
- HITL node is in the palette with the correct headphone icon
- Node added to canvas shows three labeled output handles
- All four panel sections are present and correctly labeled

**Fail:**
- Node is missing from palette
- Output handles are missing or incorrectly labeled
- Configuration panel is missing any required section
