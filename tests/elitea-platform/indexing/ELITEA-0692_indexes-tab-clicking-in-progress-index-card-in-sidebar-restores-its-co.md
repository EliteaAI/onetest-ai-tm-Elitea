---
id: ELITEA-0692
title: "[Indexes Tab] Clicking In-Progress Index Card in Sidebar Restores Its Context in Both Panels"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4838]
---
# ELITEA-0692: [Indexes Tab] Clicking In-Progress Index Card in Sidebar Restores Its Context in Both Panels

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that after navigating to the new index creation form, clicking the previously in-progress index card in the sidebar correctly restores both the center and right panels to that index's state.

**Coverage:**
- Clicking the in-progress index sidebar card switches center panel back to that index's controls
- Right panel shows the in-progress index's live progress output after clicking its card
- Panel context switching between multiple index entries works correctly bidirectionally

## Preconditions

- Logged in to {{base_url}} (Private project)
- Two index entries exist in the sidebar: one in-progress, one newly initiated
- PgVector and Embedding Model configured at project level; `index_data` tool selected in the toolkit

## Test Data

- Toolkit: any GitHub/Confluence/Jira/Sharepoint toolkit with indexing enabled
- First index data source: large enough to remain in-progress for 2+ minutes

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select a toolkit with indexing enabled → click the Indexes tab. | Indexes tab is displayed. |
| 2 | Click '+ Create New Index', fill in parameters, and click Index (first index). | First index is in-progress (spinner on card, progress messages in right panel). |
| 3 | Click '+ Create New Index' again while the first index is still in-progress. | New index card is selected; center panel shows the new index creation form. |
| 4 | In the Indexes Sidebar, click the previously in-progress index card. | The previously in-progress index card becomes the active selection. |
| 5 | Observe the center panel. | Center panel shows the in-progress index's Run/Configuration/History tabs — not the new index creation form. |
| 6 | Observe the right panel. | Right panel shows the in-progress index's progress output (live messages belonging to the first index). |

## Expected Final State

Right panel shows the in-progress index's progress output (live messages belonging to the first index).

## Pass/Fail Criteria

**Pass:**
- Clicking the in-progress card restores its controls in the center panel
- Right panel shows the correct progress output for the selected index

**Fail:**
- Center panel still shows the new index creation form after clicking the in-progress card
- Right panel shows messages from the wrong index (wrong index context)
