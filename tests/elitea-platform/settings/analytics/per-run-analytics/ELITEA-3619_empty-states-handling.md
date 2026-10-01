---
id: ELITEA-3619
title: "Empty States Handling"
priority: high
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3619: Empty States Handling

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify appropriate empty states when run has no tools, no cache usage, or no errors.

## Preconditions

- Logged into {{base_url}}
- Runs with varying data availability exist

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics for run with no tool usage. | Analytics page loads. |
| 2 | Navigate to Tools tab. | Shows empty state message (not empty table). |
| 3 | Verify message is user-friendly. | "No tools were used in this run" or similar. |
| 4 | Open Per-Run Analytics for run without cache usage. | Analytics page loads. |
| 5 | Check CACHE READ/WRITE COST cards. | Show "$0.00" (not N/A or error). |
| 6 | Check CACHE READ/WRITE TOKENS cards. | Show "0" (not empty). |
| 7 | Open Per-Run Analytics for successful run (no errors). | Analytics page loads. |
| 8 | Check ERRORS columns in Tools and Health tabs. | Show "0" with normal styling (no red). |
| 9 | Check ERROR RATE in Health tab. | Shows "0%". |

## Pass/Fail Criteria

**Pass:** All empty states handled gracefully with appropriate values/messages.
**Fail:** Empty tables, N/A values, errors, or inappropriate styling.
