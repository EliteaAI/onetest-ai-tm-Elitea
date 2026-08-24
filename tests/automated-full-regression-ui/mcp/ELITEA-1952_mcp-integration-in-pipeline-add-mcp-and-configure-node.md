---
id: ELITEA-1952
title: "MCP Integration in Pipeline — Add MCP to Tools and Configure MCP Node"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id: tests.ui.pipelines.test_pipeline_mcp_node_fresh_attach.test_mcp_node_executes_selected_tool
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1751
---

# ELITEA-1952: MCP Integration in Pipeline — Add MCP to Tools and Configure MCP Node

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a Remote MCP can be attached to a pipeline's TOOLS section, an MCP node can be added to the canvas and fully configured with a toolkit and tool, and the pipeline executes the MCP node correctly.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP (e.g., "EliteaMCP") is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline Name | autotest_mcp_pipeline |
| MCP to attach | EliteaMCP |
| Tool to select | get_auth_user |
| Output variable | user_info |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines and create a new pipeline (e.g., "autotest_mcp_pipeline") | Pipeline canvas loads |
| 2 | In the left panel, scroll to "TOOLS" section | TOOLS section is visible |
| 3 | Verify tool attachment buttons are visible: "+ Toolkit", "+ MCP", "+ Agent", "+ Pipeline" | All four buttons are present |
| 4 | Click "+ MCP" button | MCP selection dropdown/dialog appears |
| 5 | Verify MCP selection dropdown/dialog appears listing project MCPs | Available MCPs are listed |
| 6 | Select a Remote MCP (e.g., "EliteaMCP") | MCP is selected |
| 7 | Verify selected MCP appears in TOOLS list with MCP icon, name, "Show tools" link, and connection status | MCP entry shows all expected elements |
| 8 | Click "Add node" button (+ icon) in the pipeline canvas toolbar | Node type dropdown opens |
| 9 | Verify dropdown menu shows node types including MCP | MCP option is listed |
| 10 | Click "MCP" from the menu | MCP node is added to the canvas |
| 11 | Verify MCP node labeled "MCP 1" is added with Input/Output ports | Node appears with correct label and ports |
| 12 | Click on the MCP node to open its configuration panel | Configuration panel opens on the right |
| 13 | Verify MCP node config panel shows: Trigger dropdown, Toolkit dropdown, Tool dropdown, Input variable, Output variable | All config elements are present |
| 14 | In "Toolkit" dropdown — select the attached MCP (e.g., "EliteaMCP") | Toolkit is selected |
| 15 | Verify "Tool" dropdown populates with tools available from the selected MCP | Tool dropdown shows available tools |
| 16 | Select a tool from "Tool" dropdown (e.g., "get_auth_user") | Tool is selected |
| 17 | Verify Input and Output variable chips appear (e.g., Input: "input", Output: "user_info") | Variable chips are displayed |
| 18 | Connect nodes: START → MCP 1 → END | Nodes are connected |
| 19 | Save pipeline | Pipeline is saved successfully |
| 20 | Execute pipeline with a test message | Pipeline execution is triggered |
| 21 | Verify MCP node executes the selected tool and returns output | MCP node output is returned |

---

## Expected Final State

The pipeline executes successfully with the MCP node invoking the selected tool and returning output.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- MCP node is configured, pipeline saves, and MCP tool output is returned on execution.

**Fail:**
- Any step produces an error or unexpected result.
- MCP node configuration fails, pipeline does not save, or execution returns no output.
