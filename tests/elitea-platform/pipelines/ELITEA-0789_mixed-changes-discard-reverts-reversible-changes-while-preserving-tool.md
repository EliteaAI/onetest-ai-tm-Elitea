---
id: ELITEA-0789
title: "Mixed Changes — Discard Reverts Reversible Changes While Preserving Toolkit Removal"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0789: Mixed Changes — Discard Reverts Reversible Changes While Preserving Toolkit Removal

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user removes a toolkit AND makes reversible pipeline-level changes (e.g., changes the pipeline name), clicking Discard reverts only the reversible changes, while the toolkit removal remains in effect.

**Coverage:**
- Discard button activates when reversible changes are made alongside toolkit removal
- Discard reverts pipeline name to last saved value
- Discard does NOT restore the removed toolkit
- Input Mapping fields previously bound to the removed toolkit are not restored by Discard
- The same behavior applies to both Toolkit Node and LLM Node scenarios

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
| 2 | In the Toolkit Node, remove the selected toolkit (Sharepoint). | Toolkit is removed. Save and Discard remain disabled — toolkit removal is auto-saved to the backend immediately. |
| 3 | In the pipeline Name field, change the value to 'discarding changes MODIFIED'. | Name field is updated. Discard button becomes active. |
| 4 | Click Discard. | Only the name is reverted to 'discarding changes' (the last saved value). |
| 5 | Observe the pipeline Name field. | Name is reverted to 'discarding changes' (the last saved value). |
| 6 | Observe the Toolkit Node. | The toolkit is NOT present — it was auto-saved as removed before Discard was triggered. Toolkit selector is empty. |
| 7 | Observe the Input Mapping section in the Toolkit Node. | No Input Mapping fields from the removed toolkit are visible. |
| 8 | Observe the Save and Discard button states. | Both Save and Discard are INACTIVE. There are no pending changes — the reversible change was reverted by Discard and toolkit removal was already auto-saved. |
| 9 | Reload the pipeline. | Name shows 'discarding changes'. Toolkit Node is empty. No Input Mapping fields present. |

## Expected Final State

Name shows 'discarding changes'. Toolkit Node is empty. No Input Mapping fields present.

## Pass/Fail Criteria

**Pass:**
- After Discard, the pipeline Name is restored to the last saved value
- Toolkit is not present — auto-saved upon removal, not affected by Discard
- No Input Mapping fields visible
- Save and Discard buttons are both inactive after Discard (no pending changes)
- Reload confirms the correct state is persisted

**Fail:**
- Discard does not revert the pipeline Name change
- Save button is active after Discard (indicates pending unsaved changes unexpectedly remain)
- Toolkit or Input Mapping fields reappear after reload
