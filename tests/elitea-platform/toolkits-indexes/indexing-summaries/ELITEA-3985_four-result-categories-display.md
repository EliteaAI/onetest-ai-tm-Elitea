---
id: ELITEA-3985
title: "Four Result Categories Display in Indexing Summary"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, categories, results]
requirements: [EL-6229]
---
# ELITEA-3985: Four Result Categories Display in Indexing Summary

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that all four result categories (Successfully indexed, Skipped, Not indexed, Failed) appear with correct counts when indexing mixed file types.

**Coverage:**
- Successfully indexed category shows correct count
- Skipped category shows count with reasons
- Not indexed (unsupported) category shows count with formats
- Failed category shows count with file identifiers and reasons

## Preconditions

- Logged in to {{base_url}} with permissions to create indexes
- A storage bucket prepared with mixed file types:
  - 5 valid .txt files (will index successfully)
  - 2 empty .pdf files (will be skipped - no content)
  - 2 .ai files (unsupported format)
  - 1 corrupted .docx file (will fail processing)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Artifacts toolkit |
| Bucket | Prepared bucket with mixed files |
| Expected Indexed | 5 |
| Expected Skipped | 2 |
| Expected Unsupported | 2 |
| Expected Failed | 1 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select an Artifacts toolkit. | Toolkit details page opens. |
| 2 | Create a new index pointing to the prepared bucket. | Index creation initiated. |
| 3 | Wait for indexing to complete. | Status shows Completed or Partially Indexed. |
| 4 | Open Index History → click the latest entry. | Entry details panel opens. |
| 5 | Verify "Successfully indexed" section. | Shows ✓ with count = 5 files. |
| 6 | Verify "Skipped" section. | Shows ⚠ with count = 2 and reason (e.g., "empty content"). |
| 7 | Verify "Not indexed" section. | Shows ⚠ with count = 2 and unsupported formats listed (.ai). |
| 8 | Verify "Failed" section. | Shows ✕ with count = 1, file name, and failure reason. |
| 9 | Verify all four sections have appropriate visual styling. | Green for success, orange/yellow for warnings, red for failures. |

## Expected Final State

Indexing summary displays all four result categories with accurate counts, file identifiers, and human-readable reasons.

## Pass/Fail Criteria

**Pass:**
- All four categories appear when applicable
- Counts match actual file processing results
- Reasons are human-readable
- Visual styling distinguishes categories

**Fail:**
- Missing one or more categories
- Counts incorrect or mismatched
- Reasons missing or technical codes shown
- No visual distinction between categories
