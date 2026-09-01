---
id: ELITEA-3081
title: "UI Shows Reindexing In Progress Status"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, ui]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3081: UI Shows Reindexing In Progress Status

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the UI clearly indicates when reindexing is in progress and informs the user that existing data remains available for search.

**Coverage:**
- Status indicator shows "Reindexing" or similar
- Message indicates existing data remains searchable
- Progress is visible to user

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index
- Index with enough data that reindex takes noticeable time

## Test Data

- Index: Large toolkit index (to ensure reindex takes >10 seconds)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select an existing completed index. | Index displayed with ✅ Completed status. |
| 2 | Initiate Reindex. | Reindex starts. |
| 3 | Observe the index card/status indicator immediately. | Status changes to 🔄 or "Reindexing in progress". |
| 4 | Verify the status message content. | Message indicates reindexing is in progress. |
| 5 | Look for data availability message. | UI indicates "existing data remains available" or similar. |
| 6 | Observe progress indication (if any). | Progress bar, spinner, or percentage shown. |
| 7 | Wait for completion. | Status returns to ✅ Completed. |

## Expected Final State

During reindexing, UI clearly shows the operation is in progress and reassures user that data is still available.

## Pass/Fail Criteria

**Pass:**
- Status indicator clearly shows reindexing in progress
- User is informed data remains available
- Progress is visible
- Status updates to completed when done

**Fail:**
- No clear status indication
- User left uncertain about data availability
- No progress feedback
- Status stuck or incorrect
