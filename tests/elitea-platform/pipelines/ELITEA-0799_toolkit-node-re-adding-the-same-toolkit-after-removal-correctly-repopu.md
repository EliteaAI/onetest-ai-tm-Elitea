---
id: ELITEA-0799
title: "Toolkit Node — Re-adding the Same Toolkit After Removal Correctly Repopulates Input Mapping"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0799: Toolkit Node — Re-adding the Same Toolkit After Removal Correctly Repopulates Input Mapping

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that after a toolkit has been removed from a Toolkit Node and saved (clean state), re-adding the same toolkit and selecting the same tool correctly repopulates the Input Mapping section with the expected fields.

**Coverage:**
- Re-adding a previously removed toolkit repopulates the Tool dropdown
- Selecting the tool repopulates Input Mapping with the expected fields
- Values entered in Input Mapping can be saved
- Reload confirms the re-added configuration is persisted

## Preconditions

- Logged in to {{base_url}}
- A pipeline with a Toolkit Node that has no toolkit selected (toolkit was previously removed and saved — clean state)

## Test Data

- Toolkit: Sharepoint
- Tool: remove_index
- Input Mapping field: Index name
- Input Mapping value: re-added-index

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline (Toolkit Node has no toolkit). Confirm Input Mapping section is absent. | Toolkit selector is empty. Tool selector is empty. No Input Mapping fields shown. |
| 2 | Select Sharepoint from the Toolkit dropdown. | Sharepoint is selected. Tool dropdown becomes available. |
| 3 | Select remove_index from the Tool dropdown. | remove_index is selected. |
| 4 | Observe the Input Mapping section. | Input Mapping section appears with Index name field (same fields as before). |
| 5 | Enter 're-added-index' in the Index name field. | Value accepted. |
| 6 | Click Save. | Pipeline saved. |
| 7 | Reload and inspect the Toolkit Node. | Toolkit = Sharepoint, Tool = remove_index, Input Mapping Index name = re-added-index. |

## Expected Final State

Toolkit = Sharepoint, Tool = remove_index, Input Mapping Index name = re-added-index.

## Pass/Fail Criteria

**Pass:**
- Re-adding the same toolkit restores the Input Mapping section normally
- Values entered are saved and retained after reload

**Fail:**
- Input Mapping fields do not appear when re-adding the same toolkit that was previously removed
- Fields appear but are incorrectly populated or different from the expected tool parameters
