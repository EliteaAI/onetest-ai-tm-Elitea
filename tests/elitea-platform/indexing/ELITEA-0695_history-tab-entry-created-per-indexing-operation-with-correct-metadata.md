---
id: ELITEA-0695
title: "History Tab Entry Created Per Indexing Operation With Correct Metadata"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0695: History Tab Entry Created Per Indexing Operation With Correct Metadata

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that each indexing event (initial index and reindex) creates a separate clickable History tab entry with the correct event label and timestamp, and clicking each entry loads the correct run's summary.

**Coverage:**
- Initial index creates one History entry with correct event label
- Reindex creates a second History entry with a more recent timestamp
- Clicking each entry loads the summary for that specific run in the right panel

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with an existing completed index that has been reindexed at least once

## Test Data

- Existing index: mix01 with at least 2 history entries (one initial, one Reindex)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → select a completed index. | Index management panel opens. |
| 2 | Click the History tab. | History tab opens; list of past operations shown. |
| 3 | Verify at least one entry is present with an event label (e.g., 'Created') and a valid timestamp. | Entry with label and timestamp visible. |
| 4 | Trigger a Reindex via the Configuration tab; wait for completion; return to History tab. | New entry appears at the top. |
| 5 | Verify the new entry has a more recent timestamp than the previous entry. | Timestamp ordering is correct. |
| 6 | Click the older entry. | Right-panel updates to show the older run's summary. |
| 7 | Click the newer entry. | Right-panel updates to show the newer run's summary with updated counts. |

## Expected Final State

Right-panel updates to show the newer run's summary with updated counts.

## Pass/Fail Criteria

**Pass:**
- Each indexing event has a corresponding History tab entry with label and timestamp
- Clicking each entry loads the correct run's summary independently

**Fail:**
- History tab is empty despite completed indexing runs
- Clicking an older entry shows the same summary as the newest run
- Timestamps are missing or in incorrect order
