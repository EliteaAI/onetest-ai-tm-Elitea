---
id: ELITEA-0791
title: "Save Persists All Changes When Toolkit Removal and Reversible Changes Are Saved Together"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0791: Save Persists All Changes When Toolkit Removal and Reversible Changes Are Saved Together

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that after removing a toolkit from a Toolkit Node and making additional reversible changes (e.g., changing the Description), clicking Save correctly persists all changes — the toolkit removal, the Input Mapping cleanup, and the reversible field changes.

**Coverage:**
- Save activated after toolkit removal + description change
- Saved pipeline shows: toolkit removed, Input Mapping fields gone, description updated
- Reload confirms all three changes are persisted correctly

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline with a Toolkit Node (e.g., Sharepoint + remove_index)
- Save and Discard both disabled before starting

## Test Data

- Toolkit Node: Sharepoint, Tool = remove_index
- Description before: description
- Description after (test change): description UPDATED

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Confirm Save and Discard are disabled. | Save: disabled. Discard: disabled. |
| 2 | In the Toolkit Node, remove the Sharepoint toolkit. | Toolkit removed. Input Mapping fields disappear. Discard remains disabled. |
| 3 | In the Description field, change the value to 'description UPDATED'. | Description field is updated. Save button becomes active. |
| 4 | Click Save. | Pipeline is saved. |
| 5 | Reload the pipeline. | Pipeline loads. |
| 6 | Check the Toolkit Node. | Toolkit selector is empty. Tool selector is empty. No Input Mapping fields are shown. |
| 7 | Check the Description field. | Description shows 'description UPDATED'. |

## Expected Final State

Description shows 'description UPDATED'.

## Pass/Fail Criteria

**Pass:**
- After save and reload: toolkit is removed, Input Mapping is clean, and the description reflects the updated value
- No data is silently lost or rolled back

**Fail:**
- Toolkit reappears after save/reload
- Input Mapping fields reappear after save/reload
- Description is not updated (reverted to old value)
