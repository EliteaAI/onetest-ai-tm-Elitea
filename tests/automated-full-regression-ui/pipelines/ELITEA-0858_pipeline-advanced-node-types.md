---
id: ELITEA-0858
title: "Pipeline Advanced Node Types"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_advanced.TestMakeEntrypoint.test_make_node_entrypoint
  - tests.ui.pipelines.test_pipeline_advanced.TestMultiNodeTopology.test_save_multi_node_pipeline
  - tests.ui.pipelines.test_pipeline_advanced.TestMultiNodeTopology.test_three_node_chain
tags: []
requirements: []
---
# ELITEA-0858: Pipeline Advanced Node Types

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can add advanced node types (Decision, Printer, Router) to pipelines, set nodes as entrypoints, and manage multi-node chains.

**Coverage:**
- Make node an entrypoint
- Add Decision node
- Add Printer node
- Add Router node
- Create 3-node chain and save
- History tab opens

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Node types to test: Decision, Printer, Router, LLM, Code

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline. On the canvas, click the '+' button and add two LLM nodes. Connect the first LLM node to the END node by dragging from the bottom handle of the LLM node to the top handle of END. | Two LLM nodes appear on the canvas. A connection line (edge) exists between the first LLM node and END. |
| 2 | Select the second LLM node so its configuration side panel is open and look for the 'Make Entrypoint' button in the panel footer. | The 'Make Entrypoint' button is shown in the panel footer (node cards are view-only; the three-dot menu no longer carries this action). |
| 3 | Open a fresh pipeline (or create a new one). Click the '+' button and select 'Decision' from the node type menu. | A new Decision node appears on the canvas. The total node count increases by 1. |
| 4 | Click the '+' button again and select 'Printer' from the menu. | A new Printer node appears on the canvas. The total node count increases by 1. |
| 5 | Click the '+' button again and select 'Router' from the menu. | A new Router node appears on the canvas. The total node count increases by 1. |
| 6 | Create a new pipeline. Add an LLM node and a Code node. Connect them in a chain: LLM > Code > END by dragging connection handles. | Three nodes visible (LLM, Code, END) with two connection lines between them. |
| 7 | Click the Save button to save the multi-node pipeline. After saving, reload the page. | After reload, all nodes are still present. The LLM node is still visible on the canvas. |
| 8 | Click the 'History' tab at the top of the pipeline detail page. | The History tab opens and displays version history content. |

## Expected Final State

The History tab opens and displays version history content.

## Pass/Fail Criteria

**Pass:**
- All advanced node types (Decision, Printer, Router) can be added
- Make Entrypoint is available in the node side panel footer
- 3-node chain connects correctly with 2+ edges
- Multi-node pipeline persists after save + reload
- History tab is accessible

**Fail:**
- Any node type fails to add
- Node count doesn't increment after adding
- Edges not created between connected nodes
- Pipeline loses nodes after save + reload
- History tab not accessible
