---
id: ELITEA-0794
title: "Toolkit Node — Switching to a Different Toolkit Replaces Input Mapping Fields Correctly"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0794: Toolkit Node — Switching to a Different Toolkit Replaces Input Mapping Fields Correctly

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching the selected toolkit in a Toolkit Node to a different one clears the old toolkit's Input Mapping fields and shows only the new toolkit's tool-specific fields.

**Coverage:**
- Old toolkit's Input Mapping fields are cleared when a new toolkit is selected
- New toolkit's tool is selectable and populates new Input Mapping fields
- No leftover fields from the previous toolkit remain visible
- Saved and reloaded state reflects only the new toolkit's configuration

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline with a Toolkit Node: Toolkit A (e.g., Sharepoint) with a tool selected and Input Mapping populated

## Test Data

- Toolkit A (initial): Sharepoint, Tool = remove_index, Input Mapping field: Index name
- Toolkit B (replacement): a second available toolkit with a different tool (with different Input Mapping fields)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Confirm the Toolkit Node shows Sharepoint selected and Index name field in Input Mapping. | Toolkit = Sharepoint, Tool = remove_index, Input Mapping: Index name visible. |
| 2 | In the Toolkit dropdown, select Toolkit B (a different toolkit). | Toolkit B is selected. |
| 3 | In the Tool dropdown, select a tool from Toolkit B. | A tool is selected from Toolkit B. |
| 4 | Observe the Input Mapping section. | Input Mapping section shows only Toolkit B's tool parameters. No Index name or other Sharepoint-specific fields remain. |
| 5 | Click Save. | Pipeline is saved. |
| 6 | Reload the pipeline and inspect the Toolkit Node. | Toolkit Node shows Toolkit B and its tool. Input Mapping shows Toolkit B's fields only. No Sharepoint fields are present. |

## Expected Final State

Toolkit Node shows Toolkit B and its tool. Input Mapping shows Toolkit B's fields only. No Sharepoint fields are present.

## Pass/Fail Criteria

**Pass:**
- Old toolkit's Input Mapping fields are fully replaced by the new toolkit's fields after toolkit switch
- No leftover fields from Toolkit A remain after switching to Toolkit B

**Fail:**
- Fields from Sharepoint remain visible after switching to Toolkit B
- Input Mapping section shows mixed fields from both old and new toolkit
