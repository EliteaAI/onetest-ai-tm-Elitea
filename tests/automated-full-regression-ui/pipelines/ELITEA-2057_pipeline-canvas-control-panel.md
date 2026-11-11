---
id: ELITEA-2057
title: "Pipeline — Canvas Control Panel"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_canvas_zoom_and_pan.test_canvas_control_panel_zoom_out_interactivity_cards_size_and_auto_arrange
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1356
---

# ELITEA-2057: Pipeline — Canvas Control Panel

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that all canvas control panel buttons (Zoom In, Zoom Out, Fit View, Lock/Unlock, Arrange, Minimap) function correctly.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with multiple nodes is open in Flow view.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with nodes in Flow view | Pipeline canvas is displayed |
| 2 | Locate the Control Panel on the canvas with buttons: Zoom In, Zoom Out, Fit View, Lock/Unlock, Arrange, Minimap | All 6 control panel buttons are visible |
| 3 | Click "Zoom In" — verify canvas zooms in | Canvas zoom level increases |
| 4 | Click "Zoom Out" — verify canvas zooms out | Canvas zoom level decreases |
| 5 | Click "Fit View" — verify all nodes fit within viewport | All nodes are visible within the canvas viewport |
| 6 | Click "Lock canvas" (tooltip changes to "Unlock canvas"), try to drag a node, then click "Unlock canvas" and drag again | While locked, nodes cannot be dragged or connected (pan and zoom still work); after unlocking, node dragging works again |
| 7 | Click "Arrange" — the menu offers "Arrange top to bottom" and "Arrange left to right" (current orientation is checked); pick an orientation | Nodes are repositioned in an organized layout for the chosen orientation; a node dragged away returns to its arranged position when the same orientation is picked again |
| 8 | Click "Show minimap", then "Hide minimap" | The minimap appears at the bottom-right of the canvas, then disappears |

---

## Expected Final State

All canvas control panel buttons function correctly: Zoom In/Out adjust zoom level, Fit View shows all nodes, Lock/Unlock blocks and restores node dragging, Arrange repositions nodes by the chosen orientation, Minimap shows and hides the minimap.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Each control panel button produces the expected visual change on the canvas.

**Fail:**
- Any step produces an error or unexpected result.
- Any control panel button is missing or non-functional.
