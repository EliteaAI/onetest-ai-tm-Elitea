---
id: ELITEA-1955
title: "MCP Integration in Pipeline — Select MCP Directly in Node (Auto-Attach)"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id: tests.ui.pipelines_2.test_pipeline_mcp_node_empty_toolkit_before_attach.test_mcp_node_empty_toolkit_before_attach
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/4ae2f6894fa99a89b4809cf41c7b2be685c66e64
---

# ELITEA-1955: MCP Integration in Pipeline — Select MCP Directly in Node (Auto-Attach)

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the MCP node's picker always lists the project's MCPs (even when nothing is attached in TOOLS), and that picking an MCP directly in the node attaches it to the pipeline automatically, after which the node can be configured and saved.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one MCP exists in the project (e.g., "Web Search"); otherwise the picker shows "No MCPs in this project yet".

---

## Test Data

| Field | Value |
|-------|-------|
| MCP to pick | Web Search (any known project MCP) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new pipeline | Pipeline canvas loads; nothing is attached in the left TOOLS section |
| 2 | Add an MCP node | MCP node is added to the canvas |
| 3 | Open the node's MCP picker | Picker opens |
| 4 | Inspect the picker | A search textbox, a "Create new" option and a non-empty scrollable list of the project's MCPs are shown |
| 5 | Type a known MCP name (e.g., "Web Search") into the search box | The list is filtered to matching MCPs |
| 6 | Select the MCP from the filtered results | The MCP is selected |
| 7 | Check the node | The MCP is the node's selected value |
| 8 | Expand the left TOOLS section | The same MCP appears there automatically (auto-attach), without clicking "+ MCP" |
| 9 | Select a tool and fill its input mapping, save the pipeline, reload — verify configuration persists | Tool and input mapping are saved and still present after reload |

---

## Expected Final State

The MCP node is configured with an MCP and Tool, the MCP is attached in TOOLS, and the pipeline is saved successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The picker lists project MCPs before anything is attached; picking one attaches it automatically; configuration persists.

**Fail:**
- Any step produces an error or unexpected result.
- The MCP is not auto-attached to TOOLS after being picked, or configuration does not persist.
