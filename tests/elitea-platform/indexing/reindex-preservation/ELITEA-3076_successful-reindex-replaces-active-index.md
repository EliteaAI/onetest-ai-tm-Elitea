---
id: ELITEA-3076
title: "Successful Reindex Replaces Active Index"
priority: critical
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3076: Successful Reindex Replaces Active Index

**Module:** Indexing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when reindexing completes successfully, the new index version replaces the active index and becomes the searchable index.

**Coverage:**
- New index becomes active after successful reindex
- Search uses newly indexed content
- UI shows "Reindex completed successfully"

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index
- Source data has been modified (e.g., new file added to bucket) to verify new content is indexed

## Test Data

- Index: Any toolkit index with completed status
- New content: Add a file with unique keyword "NewContent6232" to the source

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab. Note the current "Last indexed" timestamp. | Timestamp noted (e.g., "2 days ago"). |
| 2 | Add new content to the source (e.g., upload file with "NewContent6232"). | New file added to source. |
| 3 | Search for "NewContent6232" before reindex. | No results found (content not yet indexed). |
| 4 | Initiate Reindex. | Reindex starts, status = 🔄 Reindexing. |
| 5 | Wait for completion. | Status = ✅ Completed. Success notification shown. |
| 6 | Verify "Last indexed" timestamp updated. | Timestamp shows current time. |
| 7 | Search for "NewContent6232" after reindex. | Search returns the newly indexed content. |

## Expected Final State

New index is active with updated content. Search returns newly indexed data. Timestamp reflects recent reindex.

## Pass/Fail Criteria

**Pass:**
- Reindex completes with ✅ Completed status
- "Last indexed" timestamp is updated
- New content is searchable after reindex
- Success notification displayed

**Fail:**
- Reindex fails or hangs
- New content not searchable after completion
- Timestamp not updated
- Old index remains active despite successful reindex
