---
id: ELITEA-4714
title: "Pipeline — New Pipeline Empty Canvas, First Node and Test Pipeline Gate"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_new_empty_canvas_first_node_test_gate.test_new_pipeline_empty_canvas_first_node_and_test_gate
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/27a0f1c5af0daed703e2526dde80870e18ac113e
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7154, EliteaAI/elitea_issues#7155, EliteaAI/elitea_issues#7156]
---

# ELITEA-4714: Pipeline — New Pipeline Empty Canvas, First Node and Test Pipeline Gate

**Module:** pipelines · **Priority:** critical · **Type:** functional

**Objective:** Verify that a new pipeline opens on an empty canvas, that the first node added becomes the entry point, that the Test Pipeline button stays disabled (with an explanatory tooltip) until the flow is configured, and that deleting all nodes returns the canvas to its empty state.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role in the project.
- At least one agent exists in the project (to configure the Agent node).

---

## Test Data

| Field | Value |
|-------|-------|
| First node type | Agent |
| Agent | any existing project agent |
| Task | `Say hello` |
| Second node type (line-release) | Printer |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Go to Pipelines and click "+ Pipeline" | The pipeline editor opens directly on the canvas (Flow view). Name is pre-filled (e.g. "Pipeline N"). The canvas shows the empty-state card with the text "Start by adding your first node to the canvas!" and a "+ Add Node" button |
| 2 | Hover the "Test Pipeline" button | "Test Pipeline" button is disabled. Tooltip (soft): "Save the pipeline to test it." |
| 3 | Click "Save"; then hover the "Test Pipeline" button | Pipeline is saved. "Test Pipeline" button is still disabled. Tooltip (soft): "Add and configure at least one node connected to End." |
| 4 | Click the "+ Add Node" button on the empty-state card | Node-type selector opens and lists all 10 types: Agent, Code, Decision, HITL, LLM, MCP, Printer, Router, State modifier, Toolkit |
| 5 | Press Esc | Node-type selector closes; empty-state card is still shown |
| 6 | Click the "+ Add Node" button again; click outside the selector | Node-type selector closes |
| 7 | Click the "+ Add Node" button again; select "Agent" | Node "Agent 1" is added to the canvas with the "Entrypoint" badge. An "End" node appears but is NOT connected. Empty-state card is no longer shown |
| 8 | Inspect the "Agent 1" card summary (`pipeline-node-summary-primary`) | Summary shows "Not configured" |
| 9 | Hover the "Test Pipeline" button | Button is disabled. Tooltip (soft): "Configure node 'Agent 1': Select an agent." |
| 10 | Click the "Agent 1" card; in the node panel select an agent from the "Agents & Pipelines" picker | Agent is selected; the card summary shows the agent name |
| 11 | Hover the "Test Pipeline" button | Button is disabled. Tooltip (soft): "Configure node 'Agent 1': Fill in the required input: task." |
| 12 | In the node panel set Task to `Say hello`; click "Save" | Pipeline is saved. "Agent 1" is now connected to "End" |
| 13 | Check the "Test Pipeline" button | "Test Pipeline" button is ENABLED (main assertion) |
| 14 | Drag a line from the "Agent 1" Output handle and release it on empty canvas space | A dropdown opens with existing nodes and a "+ Create new node" option |
| 15 | Click "+ Create new node" and select "Printer" | Node "Printer 1" is added and connected from "Agent 1" |
| 16 | Open "Agent 1" panel and click the Delete icon in the panel footer; confirm | "Agent 1" is removed. Hover "Test Pipeline" — tooltip (soft): "Set an entry point to test the pipeline." |
| 17 | Open "Printer 1" and delete it via the panel footer Delete icon (no other nodes remain besides End) | The empty-state card "Start by adding your first node to the canvas!" with the "+ Add Node" button is shown again |

---

## Expected Final State

A new pipeline starts canvas-first on the empty-state card; the first node becomes the entry point; Test Pipeline becomes enabled only once the flow is fully configured and saved; deleting all nodes returns the canvas to the empty state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Test Pipeline is disabled in steps 2–11 and enabled in step 13.
- The first node is the entry point; the empty-state card returns after all nodes are deleted.

**Fail:**
- Test Pipeline is enabled before the flow is configured, or stays disabled after it is configured and saved.
- The empty-state card, the "+ Add Node" button, or the 10 node types are missing.
- The first added node is not the entry point.

**Notes:** Tooltip texts are soft assertions — a wording change is not a failure; the enabled/disabled state is the hard assertion.
