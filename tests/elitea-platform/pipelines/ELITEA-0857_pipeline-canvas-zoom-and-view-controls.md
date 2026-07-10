---
id: ELITEA-0857
title: "Pipeline Canvas - Zoom and View Controls"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_nodes.TestCanvasInteractions.test_zoom_controls_exist
  - tests.ui.pipelines.test_pipeline_nodes.TestCanvasInteractions.test_fit_view_adjusts_viewport
tags: []
requirements: []
---
# ELITEA-0857: Pipeline Canvas - Zoom and View Controls

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify pipeline canvas zoom controls and viewport adjustment features.

**Coverage:**
- Zoom controls (zoom in/out buttons) exist
- Fit View button adjusts viewport to show all nodes

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. Open any existing pipeline to view the canvas. Look for zoom controls at the bottom-left corner: 'Zoom In' (+), 'Zoom Out' (-), and 'Fit View' buttons. | All 3 zoom control buttons are visible on the canvas. |
| 2 | Note the current zoom level and position of nodes on the canvas. | The initial viewport position is noted. |
| 3 | Add a node (e.g., LLM) to the canvas using the '+' button, so there is content to fit. | A new node is added. The canvas now has at least two elements (the new node and the END node). |
| 4 | Click the 'Fit View' button to adjust the viewport to show all nodes. | The view adjusts to fit all nodes within the visible canvas area. The zoom level or position changes from the initial state. |

## Expected Final State

The view adjusts to fit all nodes within the visible canvas area. The zoom level or position changes from the initial state.

## Pass/Fail Criteria

**Pass:**
- All 3 zoom control buttons exist and are visible
- Fit View button changes the viewport transform
- No errors during zoom/fit operations

**Fail:**
- Any zoom control button missing
- Fit View does not change viewport transform
- Canvas fails to render after zoom operations
