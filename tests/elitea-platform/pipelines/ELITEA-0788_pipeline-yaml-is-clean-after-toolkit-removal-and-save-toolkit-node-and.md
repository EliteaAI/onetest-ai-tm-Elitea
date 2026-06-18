---
id: ELITEA-0788
title: "Pipeline YAML Is Clean After Toolkit Removal and Save (Toolkit Node and LLM Node)"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0788: Pipeline YAML Is Clean After Toolkit Removal and Save (Toolkit Node and LLM Node)

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that after removing a toolkit from a Toolkit Node or LLM Node and saving, the pipeline YAML no longer contains toolkit_name, tool, input_mapping, or toolkits entries for the removed toolkit.

**Coverage:**
- Toolkit Node YAML: toolkit_name, tool, and input_mapping fields are absent after toolkit removal and save
- LLM Node YAML: the toolkits array no longer contains the removed toolkit entry after removal and save
- YAML view matches the UI state

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline containing both a Toolkit Node (Sharepoint + remove_index) and an LLM Node (with Artifacts toolkit attached)
- YAML tab is accessible in the pipeline editor

## Test Data

- Toolkit Node: Sharepoint, tool remove_index
- LLM Node: Artifacts toolkit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Click the YAML tab. | YAML is displayed. For the Toolkit Node entry: toolkit_name: sharepoint, tool: remove_index, input_mapping fields are present. For the LLM Node: toolkits array contains the Artifacts entry. |
| 2 | Switch back to the Flow tab. In the Toolkit Node, remove the Sharepoint toolkit. | Toolkit removed in the UI. Input Mapping fields disappear. |
| 3 | Click Save. | Pipeline saved. |
| 4 | Click the YAML tab. Inspect the Toolkit Node's YAML block. | The Toolkit Node YAML entry no longer contains toolkit_name, tool, or input_mapping fields. |
| 5 | Switch back to the Flow tab. In the LLM Node, remove the Artifacts toolkit. | Toolkit entry removed from LLM Node. |
| 6 | Click Save. | Pipeline saved. |
| 7 | Click the YAML tab. Inspect the LLM Node's YAML block. | The LLM Node YAML no longer contains a toolkits entry for Artifacts (or the toolkits array is empty/absent). |

## Expected Final State

The LLM Node YAML no longer contains a toolkits entry for Artifacts (or the toolkits array is empty/absent).

## Pass/Fail Criteria

**Pass:**
- YAML shows no residual toolkit references after toolkit removal and save
- YAML and UI are in sync: what is removed in the UI is also absent in the YAML

**Fail:**
- Removed toolkit's toolkit_name, tool, or input_mapping still appear in the YAML after save
- YAML contains orphaned toolkit entries not reflected in the UI
