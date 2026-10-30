---
id: ELITEA-3091
title: "Reindex Preservation — Success Flow"
priority: critical
type: automated
module: indexing/reindex-preservation
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, regression, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---

# ELITEA-3091: Reindex Preservation — Success Flow

**Module:** indexing/reindex-preservation · **Priority:** critical · **Type:** automated

**Objective:** Verify that the existing active index remains available for search throughout reindexing, and that successful reindex replaces the active index with updated content seamlessly.

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit index with ✅ Completed status and known searchable content.

## Test Data

| Variable | Description |
|----------|-------------|
| `old_search_keyword` | Unique keyword present in current indexed content |
| `expected_result_count` | Number of expected search results |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **SEARCH OLD INDEX** | | |
| 1 | Navigate to Indexes tab. Select test index with ✅ Completed status | Index displayed |
| 2 | Perform search query using `old_search_keyword` | Search returns `expected_result_count` results |
| 3 | Note search results | Results captured |
| **DURING REINDEXING** | | |
| 4 | Initiate Reindex | Status changes to 🔄 Reindexing |
| 5 | While in progress, perform same search with `old_search_keyword` | Search returns same results (old index active) |
| 6 | Verify no "index unavailable" messages | Search works normally |
| **AFTER SUCCESS** | | |
| 7 | Wait for reindex to complete | Status = ✅ Completed |
| 8 | Perform search again | Search uses NEW index content |
| 9 | Verify new index is active | Updated content searchable |

## Pass/Fail Criteria

**Pass:** Old index searchable during reindex; new index replaces old after success; seamless transition.
**Fail:** Search fails during reindex OR new index not activated after success.

## Notes

**Source:** ELITEA-3091 (searchable during), ELITEA-3093 (success replaces)
**Rationale:** Validates complete success flow: old index available → reindex → old still works → success → new active.
