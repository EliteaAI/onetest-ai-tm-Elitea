---
id: ELITEA-0790
title: "Toolkit Node — Input Mapping Fields Are Removed After Toolkit Is Removed"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5105]
---
# ELITEA-0790: Toolkit Node — Input Mapping Fields Are Removed After Toolkit Is Removed

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that removing the selected toolkit from a Toolkit Node also removes all tool-specific Input Mapping fields, leaving no orphaned fields in the UI.

**Coverage:**
- Toolkit removal clears the toolkit selector value in the Toolkit Node
- All tool-specific Input Mapping fields (e.g., `Index name`, `CUT OFF`, `EXTENDED SEARCH`, `FILTER`) disappear after toolkit removal
- No orphaned Input Mapping section remains after toolkit is removed
- Save persists the clean state
- Reload confirms no Input Mapping fields are re-introduced from backend

## Preconditions

- Logged in to {{base_url}} with project member access
- A pipeline exists and is saved with a Toolkit Node configured with: Toolkit = Sharepoint, Tool = `remove_index`, at least one Input Mapping field populated (e.g., `Index name`)
- Save and Discard buttons are disabled before starting (no pending changes)

## Test Data

- Pipeline: "Discarding changes bug" (project: bugs&features) or equivalent private pipeline
- Toolkit: Sharepoint
- Tool: remove_index
- Input Mapping field: Index name

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline in edit mode. Observe the Save and Discard button states. | Save is disabled. Discard is disabled. The Toolkit Node shows Sharepoint selected and remove_index tool selected. The Input Mapping section shows at least the Index name field. |
| 2 | In the Toolkit Node, click the remove / × button on the selected toolkit (Sharepoint). | The Sharepoint entry is removed from the Toolkit dropdown. The Toolkit field shows an empty/unselected state. |
| 3 | Observe the Tool dropdown. | Tool dropdown is empty or reset. |
| 4 | Observe the Input Mapping section of the Toolkit Node. | The Input Mapping section no longer displays any tool-specific fields (e.g., Index name). No fields from the previously selected tool remain visible. |
| 5 | Observe the Save and Discard button states. | Save remains inactive. Toolkit removal is auto-saved to the backend immediately — no manual Save is needed. |
| 6 | Reload the pipeline (navigate away and return). | The Toolkit Node shows no toolkit selected, no tool selected, and no Input Mapping fields. |

## Expected Final State

The Toolkit Node shows no toolkit selected, no tool selected, and no Input Mapping fields.

## Pass/Fail Criteria

**Pass:**
- After toolkit removal, all tool-specific Input Mapping fields are removed from the Toolkit Node
- No orphaned fields remain visible
- Save button remains inactive after removal (auto-saved immediately)
- Reloaded state shows a clean Toolkit Node with no Input Mapping section

**Fail:**
- One or more Input Mapping fields remain visible after the toolkit is removed
- Save button unexpectedly becomes active after toolkit removal
- Input Mapping fields reappear after reload
