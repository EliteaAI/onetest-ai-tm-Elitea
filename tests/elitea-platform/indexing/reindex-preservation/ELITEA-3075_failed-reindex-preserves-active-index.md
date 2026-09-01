---
id: ELITEA-3075
title: "Failed Reindex Preserves Active Index"
priority: critical
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3075: Failed Reindex Preserves Active Index

**Module:** Indexing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when reindexing fails (due to any error), the previously active index remains fully available and searchable.

**Coverage:**
- Active index is not deleted or corrupted on reindex failure
- Search continues to work after failed reindex
- Index status does not show as "broken" after failure

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index with known content
- Ability to trigger a reindex failure (e.g., disconnect integration, revoke token, or use expired credentials)

## Test Data

- Index: Toolkit index with external integration (Confluence, Jira, GitHub)
- Method to cause failure: Temporarily revoke access token or disconnect integration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab. Note the active index document count (e.g., 50 docs). | Index shows ✅ Completed with document count. |
| 2 | Perform a search query to confirm index is working. | Search returns expected results. |
| 3 | Cause a condition that will make reindex fail (e.g., revoke token in integration settings). | Integration credentials invalidated. |
| 4 | Initiate Reindex on the index. | Reindex starts, then fails with error. |
| 5 | Verify the index status after failure. | Reindex failed with explanation that include "Previously indexed data remains available for search. Check History for error details and try again after resolving the issue. Last successful indexing: ...". |
| 6 | Check the document count. | Document count unchanged (still 50 docs). |
| 7 | Perform the same search query as step 2. | Search returns the same results as before. |
| 8 | Restore integration credentials for cleanup. | Credentials restored. |

## Expected Final State

Active index remains intact with original document count. Search functionality works exactly as before the failed reindex attempt.

## Pass/Fail Criteria

**Pass:**
- Index status remains ✅ Completed (not broken)
- Document count unchanged after failure
- Search returns same results as before failure
- No data loss occurred

**Fail:**
- Index shows error/broken status
- Document count decreased or index is empty
- Search fails or returns no results
- Previously indexed data is lost
