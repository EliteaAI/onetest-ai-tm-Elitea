---
id: ELITEA-3095
title: "Automated: UI status throughout reindex lifecycle"
priority: high
type: automated
module: indexing/reindex-preservation
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, automated, regression, reindex-preservation, ui]
requirements: [EliteaAI/elitea_issues#6232]
---

# ELITEA-3095: UI status throughout reindex lifecycle

**Module:** indexing/reindex-preservation · **Priority:** high · **Type:** automated

**Objective:** Verify that the UI displays correct status indicators and messages throughout the reindex lifecycle: in progress, success, and failure states.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit index with ✅ Completed status.
- Ability to trigger both successful and failed reindex.

---

## Test Data

| Variable | Description |
|----------|-------------|
| `index_name` | Name of the test index |
| `initial_doc_count` | Document count before reindex |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Indexes tab. Verify index card shows ✅ Completed. | Status = ✅ Completed. |
| 2 | Note document count and "Last indexed" timestamp. | Metadata captured. |
| 3 | Initiate Reindex. | Reindex starts. |
| 4 | Verify index card status immediately. | Status = 🔄 "Reindexing in progress" or similar. |
| 5 | Verify UI indicates existing data remains available. | Message present about data availability. |
| 6 | Wait for successful completion. | Reindex completes. |
| 7 | Verify status updates to ✅ Completed. | Status = ✅ Completed. |
| 8 | Verify timestamp is updated. | "Last indexed" shows current time. |
| 9 | Trigger reindex failure condition. | Failure condition set. |
| 10 | Initiate Reindex again. Wait for failure. | Reindex fails. |
| 11 | Verify failure message is displayed. | "Reindex failed" message shown. |
| 12 | Verify message confirms data preservation. | "Previously indexed data remains available" present. |
| 13 | Verify index card shows ✅ Completed (not broken). | Status = ✅ (previous status, not ❌). |
| 14 | Verify document count unchanged. | Count = `initial_doc_count`. |

---

## Pass/Fail Criteria

**Pass:**
- Status shows ✅ before reindex
- Status shows 🔄 during reindex with data availability message
- Status shows ✅ after successful reindex with updated timestamp
- After failure: clear message, data preservation confirmed, status ✅ (not broken)

**Fail:**
- Incorrect status at any stage
- Missing data availability messages
- Card shows broken/error after failure
- Document count changes after failure
