---
id: ELITEA-3093
title: "Automated: Successful reindex replaces active index"
priority: critical
type: automated
module: indexing/reindex-preservation
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, automated, regression, reindex-preservation]
requirements: [EliteaAI/elitea_issues#6232]
---

# ELITEA-3093: Successful reindex replaces active index

**Module:** indexing/reindex-preservation · **Priority:** critical · **Type:** automated

**Objective:** Verify that when reindexing completes successfully, the new index version replaces the active index and becomes searchable.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit index with ✅ Completed status.
- Source data has been modified (new file added) to verify new content is indexed.

---

## Test Data

| Variable | Description |
|----------|-------------|
| `index_name` | Name of the test index |
| `new_content_keyword` | Unique keyword in newly added content |
| `initial_timestamp` | "Last indexed" timestamp before reindex |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Indexes tab. Select test index. Note `initial_timestamp`. | Timestamp noted. |
| 2 | Add new content to source with `new_content_keyword`. | New content added. |
| 3 | Search for `new_content_keyword` before reindex. | No results (content not yet indexed). |
| 4 | Initiate Reindex. | Status = 🔄 Reindexing. |
| 5 | Wait for successful completion. | Status = ✅ Completed. Success notification shown. |
| 6 | Verify "Last indexed" timestamp is updated. | Timestamp > `initial_timestamp`. |
| 7 | Search for `new_content_keyword` after reindex. | Search returns newly indexed content. |

---

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
- Old index persists despite successful reindex
