---
id: ELITEA-0706
title: "Summary Present in History Tab Entry After Reindex"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0706: Summary Present in History Tab Entry After Reindex

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that triggering a Reindex creates a new History tab entry containing a fresh summary report reflecting the current state of the source.

**Coverage:**
- Reindex creates a new History tab entry with a more recent timestamp
- New entry's summary panel shows updated per-category counts
- Summary reflects current source content — not stale data from the prior run
- Regression guard for TC-0816

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with an existing completed index
- The index was created on a mixed-file bucket (contains at least one partially-indexed or skipped file)

## Test Data

- Existing index: mix01 (from TC-01 or equivalent); bucket: summary-mix-test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → select the completed index mix01. | Index management panel opens. |
| 2 | Click the Configuration tab within the center panel. | Configuration tab shown with Reindex button. |
| 3 | Click Reindex; confirm if a dialog appears. | Reindexing starts; index card shows 🔄 In Progress. |
| 4 | Wait for the index to reach a terminal state. | Status transitions to Completed or Partially Indexed. |
| 5 | Click History tab. | History tab shows at least two entries. |
| 6 | Verify a new entry with a more recent timestamp appears at the top of the list. | New entry visible. |
| 7 | Click the new entry. | Right-panel updates to show the reindex run summary. |
| 8 | Verify the summary contains up-to-date counts and file names. | Summary reflects the current bucket state. |

## Expected Final State

Summary reflects the current bucket state.

## Pass/Fail Criteria

**Pass:**
- New History tab entry created after Reindex
- New entry's summary reflects the current bucket file state

**Fail:**
- No new History tab entry appears after Reindex completes
- History entry shows stale data from the prior run
