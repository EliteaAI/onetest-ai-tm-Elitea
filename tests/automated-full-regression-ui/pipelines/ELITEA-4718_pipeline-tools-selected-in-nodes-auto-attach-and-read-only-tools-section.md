---
id: ELITEA-4718
title: "Pipeline — Tools Selected in Nodes: Auto-Attach and Read-Only TOOLS Section"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_tools_auto_attach_read_only.test_tools_selected_in_nodes_auto_attach_and_read_only_tools
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/4cb8ce281ea8ffdada46a64dc5e3e49d01d5aceb
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7159]
---

# ELITEA-4718: Pipeline — Tools Selected in Nodes: Auto-Attach and Read-Only TOOLS Section

**Module:** pipelines · **Priority:** critical · **Type:** functional

**Objective:** Verify that toolkits, agents and pipelines are selected directly inside nodes from project-wide pickers, that selection auto-attaches them to the read-only TOOLS section in the left side panel (one attachment shared by several nodes, with "Used by"), that clearing the selection from the last node detaches it, that attach/detach are unsaved changes reverted by Discard, and that the saved YAML is clean after removal.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role.
- The project contains at least one non-MCP toolkit (e.g. "Toolkit A"), at least one MCP, at least one agent and at least one other pipeline.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Toolkit A (any tool of it) |
| Agent / pipeline to pick | any existing agent or pipeline |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new pipeline; look at the TOOLS section in the left side panel | TOOLS shows "Tools you select in nodes will appear here."; there are no "+ Toolkit" / "+ MCP" / "+ Agent" / "+ Pipeline" buttons |
| 2 | Add a Toolkit node ("+ Node" → "Toolkit"); in its panel open the Toolkit picker | The picker lists all project toolkits (no MCPs), with a search field and a "+ Create new" option |
| 3 | Select "Toolkit A" and one of its tools | "Toolkit A" appears in the TOOLS section (left side panel) with "Used by: Toolkit 1" and "Show tools" |
| 4 | Add a second Toolkit node; open its Toolkit picker | "Toolkit A" is marked "In use" |
| 5 | Select "Toolkit A" in "Toolkit 2" | TOOLS still contains ONE "Toolkit A" entry, now "Used by: Toolkit 1, Toolkit 2" |
| 6 | In the TOOLS entry click the node name "Toolkit 2" in "Used by" | "Toolkit 2" is selected on the canvas and its configuration panel opens |
| 7 | In the "Toolkit 2" panel click the "X" (clear) button next to the Toolkit field | "Toolkit A" stays in TOOLS with "Used by: Toolkit 1" |
| 8 | Open "Toolkit 1" and click the "X" (clear) button next to the Toolkit field | The "Toolkit A" entry disappears from TOOLS; "Discard" is enabled |
| 9 | Click "Discard" | "Toolkit A" is selected again on both "Toolkit 1" and "Toolkit 2", and is back in TOOLS with "Used by: Toolkit 1, Toolkit 2" |
| 10 | Clear "Toolkit A" (X) on both nodes; click "Save"; open the page "Yaml" view | Neither Toolkit node block contains `toolkit_name`, `tool` or `input_mapping` for "Toolkit A" |
| 11 | Add an Agent node; open its "Agents & Pipelines" picker | The picker lists agents and pipelines grouped under "Agents" and "Pipelines" |
| 12 | Select an agent | The agent appears in TOOLS with its version label (e.g. "base") and "Used by: Agent 1" |

---

## Expected Final State

Tools are attached only through node pickers; TOOLS is read-only and reflects attachments, shared usage and detach; attach/detach are revertible with Discard; saved YAML has no leftovers after removal.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- One attachment per item regardless of how many nodes use it; "Used by" is accurate and clickable.
- Clearing from the last node detaches; Discard restores; saved YAML is clean.

**Fail:**
- TOOLS shows add buttons, or items can be attached from TOOLS.
- Duplicate attachments are created, "Used by" is wrong, or detach / Discard do not behave as described.
- Removed toolkit keys remain in the saved YAML.

**Notes:** "Not used by any node" (orphaned attachment on an old pipeline) is covered manually.
