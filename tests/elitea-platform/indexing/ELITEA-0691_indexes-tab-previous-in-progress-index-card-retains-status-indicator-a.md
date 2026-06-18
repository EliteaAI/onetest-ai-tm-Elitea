---
id: ELITEA-0691
title: "[Indexes Tab] Previous In-Progress Index Card Retains Status Indicator After New Index Creation"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4838]
---
# ELITEA-0691: [Indexes Tab] Previous In-Progress Index Card Retains Status Indicator After New Index Creation

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that after clicking "+ Create New Index" while a previous index is in-progress, the previous index's sidebar card still shows its in-progress status indicator, and the new card is shown as the active selection.

**Coverage:**
- Previous in-progress index card retains its spinner/in-progress status indicator in the sidebar
- New index card is marked as the selected/active entry in the sidebar
- No status regression on existing index cards during simultaneous multi-index creation

## Preconditions

- Logged in to {{base_url}} (Private project)
- A toolkit with indexing enabled (GitHub, Confluence, Jira, or Sharepoint) available
- PgVector and Embedding Model configured at project level; `index_data` tool selected in the toolkit
- A data source large enough to keep the first index in-progress for 2+ minutes

## Test Data

- Toolkit: any GitHub/Confluence/Jira/Sharepoint toolkit with indexing enabled
- First index data source: large enough to remain in-progress for 2+ minutes

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select a toolkit with indexing enabled → click the Indexes tab. | Indexes tab is displayed. |
| 2 | Click '+ Create New Index', fill in parameters, and click Index to start the first index. | First index card appears. In-progress spinner is visible on it. |
| 3 | While the first index is still in-progress, click '+ Create New Index' again. | A second new index card appears in the sidebar. |
| 4 | Inspect the Indexes Sidebar — locate the first (in-progress) card. | The first index card still displays its in-progress spinner/status indicator. |
| 5 | Inspect the Indexes Sidebar — locate the newly created card. | The new index card is highlighted/selected as the active entry. |

## Expected Final State

The new index card is highlighted/selected as the active entry.

## Pass/Fail Criteria

**Pass:**
- Previous in-progress card retains its spinner/status indicator
- New card is shown as the active selection

**Fail:**
- Previous in-progress card loses its spinner or shows an incorrect status
- New card is not highlighted as active
