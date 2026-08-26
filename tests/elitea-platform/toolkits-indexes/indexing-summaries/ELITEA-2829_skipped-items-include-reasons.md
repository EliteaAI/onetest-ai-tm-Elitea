---
id: ELITEA-2829
title: "Skipped Items Include Human-Readable Reasons"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, skipped, reasons]
requirements: [EL-6229]
---
# ELITEA-2829: Skipped Items Include Human-Readable Reasons

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that items in the "Skipped" category include clear, human-readable reasons explaining why they were skipped.

**Coverage:**
- Skipped items show count
- Each skip reason is human-readable
- Different skip reasons are distinguished
- No technical codes or raw error messages

## Preconditions

- Logged in to {{base_url}} with permissions to create indexes
- A storage bucket prepared with files that will trigger different skip reasons:
  - Files excluded by extension filters (e.g., .log files when filter excludes them)
  - Files with empty or no indexable content
  - Duplicate content files (if applicable)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Artifacts toolkit with extension filters configured |
| Bucket | Bucket with files matching skip conditions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select an Artifacts toolkit. | Toolkit details page opens. |
| 2 | Configure the toolkit with extension filters (e.g., exclude .log). | Filters saved. |
| 3 | Create or reindex an index on a bucket containing files that match skip conditions. | Indexing initiated. |
| 4 | Wait for indexing to complete. | Status shows Completed or Partially Indexed. |
| 5 | Open Index History → view the summary. | Summary displays. |
| 6 | Locate the "Skipped" section. | Skipped section visible with count. |
| 7 | Verify each skip reason is displayed. | Reasons shown, e.g., "N files excluded by configured extension filters". |
| 8 | Verify reason for empty content files. | Shows "N files contained no indexable content" or similar. |
| 9 | Verify all reasons are human-readable. | No technical codes, stack traces, or raw error messages. |

## Expected Final State

Skipped items section shows counts with clear, human-readable explanations for why each group of items was skipped.

## Pass/Fail Criteria

**Pass:**
- Skipped section shows item count
- Each skip reason is human-readable
- Reasons distinguish between filter exclusions, empty content, duplicates, etc.
- No technical codes or raw messages

**Fail:**
- No reasons provided for skipped items
- Technical codes or error messages shown
- All skipped items lumped together without differentiation
- Missing skip count
