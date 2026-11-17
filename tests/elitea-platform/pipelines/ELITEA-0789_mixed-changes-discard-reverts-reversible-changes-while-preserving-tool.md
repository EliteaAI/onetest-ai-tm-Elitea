---
id: ELITEA-0789
title: "Mixed Changes — Discard Reverts Both Toolkit Removal and Other Unsaved Changes"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3, epic:7093]
requirements: [EliteaAI/elitea_issues#5105, EliteaAI/elitea_issues#7159]
---
# ELITEA-0789: Mixed Changes — Discard Reverts Both Toolkit Removal and Other Unsaved Changes

> **Updated for Pipelines 2.0:** Behaviour change (#7159). Removing a toolkit (X in the node panel) is now an unsaved change, not an auto-save. Discard becomes enabled and restores the toolkit along with other unsaved changes. Save persists the removal.

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user removes a toolkit from a node AND makes another unsaved change (e.g., changes the pipeline name), Discard reverts both — the name and the toolkit removal.

**Coverage:**
- Toolkit removal (X) activates Save and Discard
- Discard reverts the pipeline name to the last saved value
- Discard restores the removed toolkit, its tool and Input Mapping
- Discard restores the toolkit entry in the left TOOLS section
- Save after removal persists it

## Preconditions

- Logged in to {{base_url}}
- A saved pipeline with a Toolkit Node that has a toolkit and tool configured
- Save and Discard both disabled before starting

## Test Data

- Pipeline name before: discarding changes
- Pipeline name after (test change): discarding changes MODIFIED
- Toolkit Node: Sharepoint, tool remove_index

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Confirm Save and Discard are both disabled. | Save: disabled. Discard: disabled. |
| 2 | Open the Toolkit Node panel and click the X (clear) button next to the Toolkit field (Sharepoint). | Toolkit is removed from the node; tool and Input Mapping fields disappear. Sharepoint disappears from the TOOLS section (no other node uses it). **Save and Discard become enabled.** |
| 3 | In the pipeline Name field, change the value to 'discarding changes MODIFIED'. | Name field is updated. Save and Discard remain enabled. |
| 4 | Click Discard. | All unsaved changes are reverted. |
| 5 | Observe the pipeline Name field. | Name is reverted to 'discarding changes' (the last saved value). |
| 6 | Open the Toolkit Node panel. | Toolkit Sharepoint and tool remove_index are restored on the node. |
| 7 | Observe the Input Mapping section and the TOOLS section. | Input Mapping fields are restored. Sharepoint is listed again in TOOLS with "Used by: <node name>". |
| 8 | Observe the Save and Discard button states. | Both Save and Discard are disabled — no pending changes. |
| 9 | Remove the toolkit again (X), then click Save. Reload the pipeline. | Name shows 'discarding changes'. Toolkit Node is empty, no Input Mapping fields; Sharepoint is not in TOOLS. |

## Expected Final State

After Discard, both the name and the toolkit are restored; after a removal + Save, the removal persists on reload.

## Pass/Fail Criteria

**Pass:**
- Toolkit removal enables Save and Discard
- Discard restores the pipeline Name and the removed toolkit (tool, Input Mapping, TOOLS entry)
- Save and Discard are disabled after Discard
- Removal + Save persists after reload

**Fail:**
- Toolkit removal does not enable Discard
- Discard does not restore the toolkit or the Name
- Toolkit reappears after removal + Save + reload
