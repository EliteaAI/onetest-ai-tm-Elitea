---
id: ELITEA-2010
title: "Pipeline with Toolkit Node"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_toolkit_node_config_and_input_mapping.test_toolkit_node_config_and_input_mapping
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/10d28ba6
---

# ELITEA-2010: Pipeline with Toolkit Node

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a Toolkit node can be added to a pipeline, configured with a toolkit and tool selection, input mappings populated with tool-specific parameters, and that all configuration persists after saving and reloading.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit (e.g., "SDConfluence") is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit name | SDConfluence |
| Tool name | search_index |
| QUERY Type | F-String |
| QUERY Value | {input} error |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline | Pipeline is created and opened in the editor |
| 2 | Add a Toolkit node via "Add node" → "Toolkit" | Toolkit node appears on the canvas |
| 3 | Click Toolkit node — verify panel shows: Toolkit dropdown, Tool dropdown, Input, Output, INPUT MAPPING (REQUIRED N), INPUT MAPPING (OPTIONAL N), Structured output | All listed sections are present in the panel |
| 4 | In the node's Toolkit picker (search box, "Create new", project-wide list) select an existing toolkit (e.g., "SDConfluence") | Toolkit is selected on the node and appears automatically in the left TOOLS section (auto-attach; no "+ Toolkit" button) |
| 5 | Select a tool from "Tool" dropdown (e.g., "search_index") — verify INPUT MAPPING sections populate with tool-specific parameters | INPUT MAPPING sections appear with tool-specific parameter fields |
| 6 | In INPUT MAPPING (REQUIRED): set QUERY Type to "F-String", Value: "{input} error" | QUERY mapping is configured with f-string value |
| 7 | Set Input and Output comboboxes | Input and Output variables are configured |
| 8 | Save pipeline | Pipeline saves without errors |
| 9 | Reload — verify Toolkit, Tool selection, and INPUT MAPPING values persist | All Toolkit node configuration persists after reload |

---

## Expected Final State

The Toolkit node is fully configured with the "SDConfluence" toolkit, "search_index" tool, QUERY mapping (F-String/"{input} error"), and Input/Output variables, all persisting after save and reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toolkit, Tool selection, INPUT MAPPING, Input, and Output all persist correctly after reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any toolkit node configuration field is lost after saving.
