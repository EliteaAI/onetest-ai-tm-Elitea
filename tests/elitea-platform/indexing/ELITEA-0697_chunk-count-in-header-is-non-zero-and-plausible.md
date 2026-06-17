---
id: ELITEA-0697
title: "Chunk Count in ✅ Header Is Non-Zero and Plausible"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0697: Chunk Count in ✅ Header Is Non-Zero and Plausible

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify the (M chunks) value in the ✅ Successfully indexed N documents (M chunks). line is non-zero and within a plausible range for the indexed content.

**Coverage:**
- Chunk count M is non-zero after indexing at least 1 valid file
- M is within a plausible range relative to file count and size
- Chunk count shown correctly after both initial index and reindex

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled; bucket with known small files

## Test Data

- Bucket: chunk-count-test; index name: cc01
- Files: 5 × .txt files of approximately 1 KB each

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → create index cc01 → click Index. | Indexing starts. |
| 2 | Wait for ✅ Completed; click History tab → select the latest entry. | Summary panel opens. |
| 3 | Read the full ✅ line (e.g., ✅ Successfully indexed 5 documents (M chunks).). | Line is present with both document count and chunk count. |
| 4 | Verify M > 0. | Chunk count is a positive integer. |
| 5 | Verify M is within a plausible range for 5 × 1 KB files (e.g., between 5 and 50 chunks with default chunking config). | Chunk count is reasonable. |

## Expected Final State

Chunk count is reasonable.

## Pass/Fail Criteria

**Pass:**
- ✅ line present; document count = 5; chunk count M > 0 and plausible

**Fail:**
- Chunk count = 0 for a non-empty valid-file batch
- Chunk count is implausibly large (e.g., 10 000+) for 5 small text files
