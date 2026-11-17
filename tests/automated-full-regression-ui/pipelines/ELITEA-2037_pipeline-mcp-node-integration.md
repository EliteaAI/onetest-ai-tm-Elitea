---
id: ELITEA-2037
title: "Pipeline — MCP Node Integration"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7159]
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_mcp_node_fresh_attach.test_mcp_node_fresh_attach
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/3d71a16b
---

# ELITEA-2037: Pipeline — MCP Node Integration

> **Updated for Pipelines 2.0:** the "+ MCP" button in TOOLS no longer exists — the MCP is picked in the MCP node's own picker and auto-attached (#7159). Merged in ELITEA-1953 (change input-mapping type) and ELITEA-1952 (run the pipeline, MCP output returned); both retired. The automation spec already uses the node picker; new steps 10 and 14–15 need to be added to it.

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that an MCP is selected directly in an MCP node (auto-attached to the TOOLS section), that the node is configured with tool-specific INPUT MAPPING including the mapping type, that all configuration persists after save and reload, and that the pipeline executes the MCP tool.

---

## Preconditions

- User is logged in to the Elitea platform.
- An MCP (e.g., "WebSearch") is available and logged in in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| MCP name | WebSearch |
| Tool | any tool with at least one required input |
| Mapping type change | Fixed → Variable (`input`) |
| Run message | `test` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline (or create a new one) | Pipeline is open; TOOLS section (left side panel) shows no "+ MCP" button |
| 2 | Click "+ Node" → select "MCP" | MCP node "MCP 1" is added and its configuration panel opens |
| 3 | Verify the panel shows: MCP picker, Tool dropdown, Input, Output, INPUT MAPPING (REQUIRED N), INPUT MAPPING (OPTIONAL N), Structured output | All listed sections are present |
| 4 | Open the MCP picker | The picker lists the project MCPs, with a search field |
| 5 | Select "WebSearch" | "WebSearch" is selected in the node |
| 6 | Check the TOOLS section (left side panel) | "WebSearch" is listed automatically with "Used by: MCP 1" |
| 7 | Select a tool from the "Tool" dropdown | INPUT MAPPING sections populate with the tool's parameters, each with its name and type |
| 8 | Configure the required INPUT MAPPING fields (Type + Value) | INPUT MAPPING values are set |
| 9 | Set the Input / Output comboboxes | Input and Output variables are configured |
| 10 | For one required parameter change Type from "Fixed" to "Variable" and select `input` | The type selector updates and the value field becomes a state-variable selector set to `input` |
| 11 | Connect "MCP 1" → End (if not connected); click "Save" | Pipeline saves without errors |
| 12 | Reload; click "MCP 1" | MCP, Tool, INPUT MAPPING values and the changed mapping type persist |
| 13 | Check the TOOLS section | "WebSearch" is still listed, "Used by: MCP 1" |
| 14 | Click "Test Pipeline"; send `test` | The pipeline runs; the thinking steps show the MCP tool call |
| 15 | Wait for completion | The MCP node returns output and the run completes without errors |

---

## Expected Final State

The MCP is selected in the node and auto-attached to TOOLS; the MCP node is fully configured (including a changed mapping type) and persists after reload; the pipeline executes the MCP tool and returns output.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Auto-attach to TOOLS works; configuration including the mapping type persists after reload; the MCP tool executes.

**Fail:**
- The MCP cannot be selected in the node, or is not attached to TOOLS.
- Any MCP node configuration is lost after saving.
- The pipeline run fails or the MCP tool is not called.
