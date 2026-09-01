---
id: ELITEA-3086
title: "Pending Index Created Separately from Active Index"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, architecture]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3086: Pending Index Created Separately from Active Index

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that during reindexing, a new pending index version is created separately without modifying or marking the active index for deletion.

**Coverage:**
- Build-then-replace architecture is implemented
- Active index is not modified during reindexing
- Pending index is separate from active
- Active index is not marked for deletion prematurely

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index with known document count
- Ability to monitor index state (via API or database if needed)

## Test Data

- Index: Any toolkit index with 50+ documents
- Note original index metadata before test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select an index. Note document count (e.g., 50). | Document count noted. |
| 2 | Note the index metadata/version if visible. | Metadata noted. |
| 3 | Initiate Reindex. | Reindex starts. |
| 4 | While reindex is in progress (20-50% complete), verify: | - |
|   | a) Active index document count | Still shows 50 (unchanged). |
|   | b) Search functionality | Returns results from active index. |
|   | c) Index status | Shows reindexing, not deleting/rebuilding. |
| 5 | Allow reindex to complete successfully. | ✅ Completed. |
| 6 | Verify new index replaced the old one. | Document count may be same or updated. |
| 7 | Verify no orphaned index versions remain. | Only one active index exists. |

## Expected Final State

Active index remained intact throughout reindexing. New index cleanly replaced it upon completion.

## Pass/Fail Criteria

**Pass:**
- Active index unchanged during reindexing
- No premature deletion of active index
- Clean replacement upon success
- No orphaned index versions

**Fail:**
- Active index modified or deleted during reindexing
- Search returns partial results during process
- Multiple index versions left orphaned
- Data inconsistency detected
