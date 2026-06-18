---
id: ELITEA-0694
title: "[Indexes Tab] Center and Right Panels Both Update When \"+\" Is Clicked During In-Progress Index"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4838]
---
# ELITEA-0694: [Indexes Tab] Center and Right Panels Both Update When "+" Is Clicked During In-Progress Index

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking "+ Create New Index" while a previous index is in-progress updates both the center panel (to the new index creation form) and the right panel (to a blank/empty state), not the previous index's state.

**Coverage:**
- Center panel switches from in-progress index controls to the new index creation form
- Right panel clears all previous index progress messages and shows an empty/no-progress state
- Both panels reflect the newly created index entry simultaneously

## Preconditions

- Logged in to {{base_url}} (Private project)
- A toolkit with indexing enabled (GitHub, Confluence, Jira, or Sharepoint) available
- PgVector and Embedding Model configured at project level; `index_data` tool selected in the toolkit
- At least one index is currently in the "in-progress" state (spinner visible in its sidebar card)

## Test Data

- Toolkit: any GitHub/Confluence/Jira/Sharepoint toolkit with indexing enabled
- First index data source: large enough to remain in-progress for 2+ minutes (e.g., GitHub repo with 50+ files)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select a toolkit with indexing enabled → click the Indexes tab. | Indexes tab is shown with the three-panel layout (sidebar, center panel, right panel). |
| 2 | Click '+ Create New Index', fill in the required parameters for the first index, and click Index. | First index card appears in the sidebar. Progress spinner is visible on the card. Progress messages begin appearing in the right (Chat) panel. |
| 3 | While the first index is still in-progress (spinner visible on its sidebar card), click '+ Create New Index' again. | A new index card appears in the sidebar and is shown as the selected/active entry. |
| 4 | Observe the center (Index Management) panel. | The center panel displays the new index creation form — NOT the previous index's Run/Configuration/History tabs or controls. |
| 5 | Observe the right (Chat) panel. | The right panel is blank or shows an empty/no-progress state — no messages from the previous in-progress index are shown. |

## Expected Final State

The right panel is blank or shows an empty/no-progress state — no messages from the previous in-progress index are shown.

## Pass/Fail Criteria

**Pass:**
- Center panel shows the new index creation form after clicking "+"
- Right panel is blank or shows empty state for the new index
- Both panels switch simultaneously upon clicking "+"

**Fail:**
- Center panel still shows the previous in-progress index's controls or Run tab
- Right panel still shows progress messages belonging to the previous index
- Either panel fails to update after clicking "+"
