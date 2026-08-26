---
id: ELITEA-2811
title: "Chunk Counts Not Displayed in User-Facing Summaries"
priority: medium
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, chunks, user-experience]
requirements: [EL-6229]
---
# ELITEA-2811: Chunk Counts Not Displayed in User-Facing Summaries

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that chunk counts (e.g., "965 chunks") are not displayed in user-facing indexing summaries.

**Coverage:**
- No "chunks" mention in Index History summaries
- No "chunks" mention in Toolkit Run History summaries
- Technical details may remain in expandable/debug sections only
- User sees file/item counts, not chunk counts

## Preconditions

- Logged in to {{base_url}}
- An index with completed indexing operation

## Test Data

| Field | Value |
|-------|-------|
| Index | Any completed index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select a toolkit. | Toolkit details page opens. |
| 2 | Open an index → navigate to Index History. | Index History displays. |
| 3 | Select the most recent indexing event. | Entry details panel opens. |
| 4 | Review the entire summary output. | Summary text visible. |
| 5 | Search/scan for any mention of "chunks" in the summary. | NO "chunks" mention in primary output. |
| 6 | Verify counts shown are file/item counts, not chunk counts. | Shows "N files indexed" not "N chunks created". |
| 7 | Navigate back to toolkit → click "Run History". | Toolkit Run History displays. |
| 8 | Locate an index_data tool execution entry. | Entry found. |
| 9 | View the output section. | Output displays. |
| 10 | Search/scan for any mention of "chunks" in the output. | NO "chunks" mention in user-facing output. |
| 11 | If expandable technical/debug sections exist, chunks may appear there only. | Chunks acceptable only in hidden technical sections. |

## Expected Final State

User-facing indexing summaries show file/item counts without any mention of internal chunk counts.

## Pass/Fail Criteria

**Pass:**
- No "chunks" in Index History summary
- No "chunks" in Toolkit Run History output
- File/item counts shown instead
- Technical chunk details hidden (if present)

**Fail:**
- "chunks" mentioned in Index History
- "chunks" mentioned in Toolkit Run History
- Summary shows "N chunks" instead of "N files"
- Chunk counts prominently displayed
