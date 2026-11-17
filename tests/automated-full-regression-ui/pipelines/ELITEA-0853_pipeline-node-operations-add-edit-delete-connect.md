---
id: ELITEA-0853
title: "Pipeline Node Operations - Add, Edit, Delete, Connect"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_nodes.TestAddNode.test_add_human_in_the_loop_node_and_connect_to_end
tags: [epic:7093]
requirements: [EliteaAI/elitea_issues#7154, EliteaAI/elitea_issues#7157]
---
# ELITEA-0853: Pipeline Node Operations - Add, Edit, Delete, Connect

> **Updated for Pipelines 2.0:** Nodes are added via **+ Add Node** / **+ Node** (#7154). Cards are view-only, so renaming is done in the node panel's Name field and deleting with the panel footer Delete (#7157). The "custom nodes" wording is replaced with LLM/Code.

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify core pipeline node operations: adding LLM/Code nodes, editing node properties in the node panel, deleting nodes safely, and connecting nodes.

**Coverage:**
- Add LLM node to pipeline
- Add Code node to pipeline
- Edit node name (node panel)
- Node default name matches type (LLM, Code)
- Delete node via the node panel footer
- Delete node does not remove END node
- Connect node to END
- Connect LLM and Code nodes

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one pipeline exists (create one manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Node types to test: LLM, Code
- Rename test value: MyCustomLLM

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline. Click **+ Node** in the toolbar (or **+ Add Node** on an empty canvas) and select 'LLM'. | A new LLM node appears on the canvas. The total node count increases by 1. |
| 2 | Click **+ Node** again and select 'Code'. | A new Code node appears on the canvas. The total node count increases by 1. |
| 3 | Click the LLM node card to open its panel. In the Name field, type 'MyCustomLLM'. | The card title updates to show 'MyCustomLLM'. |
| 4 | Add a second LLM node. Check the default names of the LLM nodes. | The nodes follow a sequential naming pattern (e.g., 'LLM 1', 'LLM 2'). |
| 5 | Add an LLM node. Note the total node count. Click its card, click the Delete icon in the panel footer, and confirm if prompted. | The node is removed. The total node count decreases by 1. |
| 6 | Add a Code node, then delete it the same way. Verify the END node is still present on the canvas. | The END node remains on the canvas after deleting the Code node. |
| 7 | Add an LLM node. Click 'Fit View' to see all nodes. Drag a connection from the LLM node's Output to the END node's Input. | A connection line (edge) appears between the LLM node and the END node. |
| 8 | Add both an LLM node and a Code node. Drag a connection from the LLM node's Output to the Code node's Input. | A connection line appears between the LLM and Code nodes. |

## Expected Final State

A connection line appears between the LLM and Code nodes.

## Pass/Fail Criteria

**Pass:**
- LLM and Code nodes can be added with correct type identifiers
- Node rename in the panel updates the card and data-id correctly
- Default naming follows sequential pattern (LLM 1, LLM 2)
- Node deletion removes exactly the target node, preserves END
- Connections create visible edges between nodes

**Fail:**
- Node addition fails or wrong type created
- Rename doesn't persist or breaks data-id
- Delete removes wrong node or END node
- Connection drag doesn't create edge
- Node count inconsistency after operations
