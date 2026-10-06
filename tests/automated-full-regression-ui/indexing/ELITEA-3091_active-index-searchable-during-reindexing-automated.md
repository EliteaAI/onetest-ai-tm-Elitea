---
id: ELITEA-3091
title: "Automated: Active index searchable during reindexing"
priority: critical
type: automated
module: indexing/reindex-preservation
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, regression, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---

# ELITEA-3091: Active index searchable during reindexing

**Module:** indexing/reindex-preservation · **Priority:** critical · **Type:** automated

**Objective:** Verify that the existing active index remains available for search throughout the entire reindexing process.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit index with ✅ Completed status and known searchable content.
- Index contains documents with a known unique keyword for search verification.

---

## Test Data

| Variable | Description |
|----------|-------------|
| `index_name` | Name of the test index |
| `search_keyword` | Unique keyword present in indexed content |
| `expected_result_count` | Number of expected search results |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Indexes tab. Select the test index. | Index displayed with ✅ Completed status. |
| 2 | Perform search query using `search_keyword` via Agent chat or Test Settings. | Search returns `expected_result_count` results. |
| 3 | Note the search results (titles, snippets). | Results captured for comparison. |
| 4 | Initiate Reindex on the index. | Status changes to 🔄 Reindexing. |
| 5 | While reindex is in progress, perform the same search query. | Search returns same `expected_result_count` results. |
| 6 | Compare results with step 3. | Results are identical. |
| 7 | Wait for reindex to complete. | Status = ✅ Completed. |

---

## Pass/Fail Criteria

**Pass:**
- Search returns expected results during reindexing
- Results are consistent with pre-reindex state
- No errors or timeouts during search

**Fail:**
- Search returns empty or different results during reindexing
- Search errors or timeouts occur
- Results are inconsistent
