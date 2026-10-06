---
id: ELITEA-2322
title: "Tools tab displays Most Popular Tools bar chart and Tool Details table"
priority: medium
type: functional
module: settings-analytics
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2322: Tools tab displays Most Popular Tools bar chart and Tool Details table

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Tools tab displays Most Popular Tools bar chart and Tool Details table. Success is confirmed when verify the table is paginated with rows per page selector and page range label.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics → Tools tab | Target page/section loads successfully. |
| 2 | Verify the "Most Popular Tools" bar chart is shown with subtitle "Top N by usage" and tool names on X axis | Condition holds as described. |
| 3 | Verify each bar has a distinct color | Condition holds as described. |
| 4 | Verify the "Tool Details" table is shown with subtitle showing tool count (e.g., "17 tools") | Condition holds as described. |
| 5 | Verify the table has columns: TOOL, CALLS, USERS, AVG LATENCY, ERRORS | Condition holds as described. |
| 6 | Verify ERRORS column value is shown in red when greater than 0 | Condition holds as described. |
| 7 | Verify a "Search by tool name" input is present | Condition holds as described. |
| 8 | Verify the table is paginated with Rows per page selector and page range label | Condition holds as described. |

---

## Expected Final State

Verify the table is paginated with Rows per page selector and page range label.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Tools tab displays Most Popular Tools bar chart and Tool Details table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
