---
id: ELITEA-3089
title: "Index Card Shows Correct Status Throughout Lifecycle"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, ui]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3089: Index Card Shows Correct Status Throughout Lifecycle

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the index card in the Indexes tab displays the correct status throughout the reindex lifecycle: before, during, after success, and after failure.

**Coverage:**
- Index card status before reindex
- Index card status during reindex
- Index card status after successful reindex
- Index card status after failed reindex (not broken)

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index
- Ability to cause reindex failure

## Test Data

- Index: Any toolkit index
- Note: Test requires multiple reindex cycles

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab. Observe index card. | Card shows ✅ Completed status. |
| 2 | Note document count and last indexed time. | Metadata noted. |
| 3 | Initiate Reindex. | Reindex starts. |
| 4 | Observe index card immediately. | Status shows 🔄 Reindexing or "In Progress". |
| 5 | Wait for successful completion. | Reindex completes. |
| 6 | Observe index card. | Status shows ✅ Completed, timestamp updated. |
| 7 | Cause reindex failure condition. | Condition set. |
| 8 | Initiate Reindex again. Wait for failure. | Reindex fails. |
| 9 | Observe index card after failure. | Status shows ✅ Completed (previous status), NOT ❌ broken. |
| 10 | Verify card still shows previous document count. | Count unchanged from successful reindex. |

## Expected Final State

Index card correctly reflects status at each stage. After failure, card shows healthy (not broken) status with preserved metadata.

## Pass/Fail Criteria

**Pass:**
- Card shows ✅ before reindex
- Card shows 🔄 during reindex
- Card shows ✅ after successful reindex
- Card shows ✅ after failed reindex (not broken)
- Document count preserved after failure

**Fail:**
- Incorrect status at any stage
- Card shows broken/error after failure
- Document count lost after failure
- Card doesn't update appropriately
