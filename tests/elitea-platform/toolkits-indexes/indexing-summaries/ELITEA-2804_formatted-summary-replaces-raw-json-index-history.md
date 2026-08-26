---
id: ELITEA-2804
title: "Formatted Summary Replaces Raw JSON in Index History"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, index-history, formatting]
requirements: [EL-6229]
---
# ELITEA-2804: Formatted Summary Replaces Raw JSON in Index History

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Index History displays a user-readable formatted summary instead of raw JSON output.

**Coverage:**
- Raw JSON like `{"indexed": N, "total": M}` is replaced
- Formatted summary shows categorized results
- Summary includes success/warning/error sections
- No chunk counts in user-facing output

## Preconditions

- Logged in to {{base_url}}
- An Artifacts toolkit with a completed index exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any Artifacts toolkit with completed index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes. | Toolkits list displays. |
| 2 | Select a toolkit that has an existing index. | Toolkit details page opens. |
| 3 | Click on an index to open Index Details. | Index details page opens. |
| 4 | Click "View index history" or navigate to History tab. | Index History page displays. |
| 5 | Select the most recent indexing event entry. | Entry details panel opens. |
| 6 | Observe the output content. | Output displays formatted summary. |
| 7 | Verify NO raw JSON like `{"indexed": 179, "total": 199}` appears. | Raw JSON format is NOT present. |
| 8 | Verify the summary shows categorized sections. | Sections visible: ✓ Successfully indexed, ⚠ Skipped (if any), ⚠ Not indexed (if any), ✕ Failed (if any). |
| 9 | Verify NO "chunks" count appears in the summary. | No mention of chunks in user-facing output. |

## Expected Final State

Index History displays a human-readable formatted summary with categorized results instead of raw JSON.

## Pass/Fail Criteria

**Pass:**
- Raw JSON format replaced with formatted summary
- Summary shows distinct category sections
- Each category has count and relevant details
- No chunk counts in user-facing output

**Fail:**
- Raw JSON like `{"indexed": N, "total": M}` still displayed
- No formatted summary visible
- Missing category breakdowns
- Chunk counts appear in primary output
