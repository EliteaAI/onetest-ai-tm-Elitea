---
id: ELITEA-0693
title: "[Indexes Tab] Normal \"+ Create New Index\" Flow Works When No Index Is In-Progress"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4838]
---
# ELITEA-0693: [Indexes Tab] Normal "+ Create New Index" Flow Works When No Index Is In-Progress

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the fix does not regress the baseline behavior: clicking "+ Create New Index" when all existing indexes are in a terminal state correctly focuses both panels on the new entry.

**Coverage:**
- Center panel shows new index creation form when no index is in-progress
- Right panel is blank/empty for new index in baseline state
- Regression guard for the panel focus fix applied to issue #4838

## Preconditions

- Logged in to {{base_url}} (Private project)
- A toolkit with at least one completed/stopped/failed index available
- No index is currently in-progress
- PgVector and Embedding Model configured; `index_data` tool selected

## Test Data

- Toolkit: any GitHub/Confluence/Jira/Sharepoint toolkit with at least one completed or stopped index
- Existing index status: completed or stopped (no spinner on any card)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select a toolkit with at least one completed/stopped index → click the Indexes tab. | Indexes tab is shown. All sidebar cards display a terminal status (no spinner). |
| 2 | Click the '+ Create New Index' button. | A new index card appears in the sidebar and is selected as the active entry. |
| 3 | Observe the center (Index Management) panel. | Center panel shows the new index creation form with empty/default input fields. |
| 4 | Observe the right (Chat) panel. | Right panel is blank or shows an empty/no-progress state. |

## Expected Final State

Right panel is blank or shows an empty/no-progress state.

## Pass/Fail Criteria

**Pass:**
- Center panel shows the new index creation form
- Right panel is blank for the new entry

**Fail:**
- Center panel shows a previously completed index's state
- Right panel shows output from a different index
