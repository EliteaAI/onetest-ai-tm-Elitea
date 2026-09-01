---
id: ELITEA-3074
title: "Active Index Remains Searchable During Reindexing"
priority: critical
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3074: Active Index Remains Searchable During Reindexing

**Module:** Indexing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the existing active index remains available for search throughout the entire reindexing process (manual or scheduled).

**Coverage:**
- Search returns results from active index while reindex is in progress
- No interruption to search functionality during reindexing
- Build-then-replace approach keeps active index intact

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index with known searchable content
- At least one document with unique searchable keyword (e.g., "TestKeyword123")

## Test Data

- Index: Any toolkit index with completed status
- Search query: Known keyword that exists in indexed content

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Indexes tab. Note the active index with ✅ Completed status. | Index displayed with document count. |
| 2 | Perform a search query using Index Data tool (via Agent chat or Test Settings). | Search returns expected results from the active index. |
| 3 | Initiate Reindex on the same index. | Status changes to 🔄 Reindexing. |
| 4 | While reindex is in progress, perform the same search query again. | Search returns the same results as before reindex started. |
| 5 | Repeat search 2-3 times during reindexing. | Each search returns consistent results from active index. |

## Expected Final State

Search functionality works without interruption throughout reindexing. Results are consistent with pre-reindex state.

## Pass/Fail Criteria

**Pass:**
- All search queries during reindexing return expected results
- No errors, timeouts, or empty results during reindexing
- Search response time is not significantly degraded

**Fail:**
- Search returns empty results during reindexing
- Search errors or timeouts occur
- Results are inconsistent or missing data
