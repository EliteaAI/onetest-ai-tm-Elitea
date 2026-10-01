---
id: ELITEA-3629
title: "Empty States and Edge Cases"
priority: high
type: functional
module: per-run-analytics
status: draft
execution_type: automated
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3629: Empty States and Edge Cases

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Regression

**Objective:** Verify Per-Run Analytics handles empty states gracefully (no tools, no cache, no errors).

## Preconditions

- Logged into {{base_url}}
- Test data: runs with different characteristics:
  - Run A: no tool usage (simple chat)
  - Run B: no cache usage
  - Run C: no errors (successful run)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics for Run A (no tools). | Analytics page loads. |
| 2 | Navigate to Tools tab. | Tab loads. |
| 3 | Verify empty state message displayed. | User-friendly message (not empty table). |
| 4 | Click Export button. | Export completes. |
| 5 | Verify export handles empty Tools sheet. | Sheet present with appropriate empty state. |
| 6 | Open Per-Run Analytics for Run B (no cache). | Analytics page loads. |
| 7 | Verify CACHE READ COST and CACHE WRITE COST show "$0.00". | Zero values, not N/A. |
| 8 | Navigate to Tokens tab. | Tab loads. |
| 9 | Verify CACHE READ TOKENS and CACHE WRITE TOKENS show "0". | Zero values, not empty. |
| 10 | Open Per-Run Analytics for Run C (no errors). | Analytics page loads. |
| 11 | Navigate to Tools tab. | Tab loads. |
| 12 | Verify ERRORS column shows "0" (no red styling). | Normal styling for zero. |
| 13 | Navigate to Health tab. | Tab loads. |
| 14 | Verify ERROR RATE shows "0%". | Percentage format with zero. |
| 15 | Verify green status indicators for 0% error rate. | Green dots displayed. |

## Automation Notes

- Pre-create test data with specific characteristics
- Verify visual styling (colors) for status indicators
- Parse Excel sheets to verify empty state handling

## Pass/Fail Criteria

**Pass:** All empty states handled gracefully with appropriate values/messages.
**Fail:** Empty tables, N/A values, or inappropriate styling.
