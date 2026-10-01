---
id: ELITEA-3610
title: "Run Header Format and Executed Version Display"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3610: Run Header Format and Executed Version Display

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify run header displays correct format and shows executed version (not current editor version).

## Preconditions

- Logged into {{base_url}}
- Agent with multiple saved versions and runs from different versions exists

## Test Data

- Agent with versions: "base", "v2"
- Run executed with "base" version
- Current editor shows "v2" version

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics for an Agent run. | Analytics page loads. |
| 2 | Verify header format. | Shows: "Run: DD MMM YYYY, HH:MM AM/PM · Version: [version_name]" |
| 3 | Verify date matches selected run's execution date. | Date is correct. |
| 4 | Verify time format includes AM/PM. | Time shows 12-hour format with AM/PM. |
| 5 | Verify Agent editor currently has different version than run. | Editor shows non-base version. |
| 6 | Verify header shows EXECUTED version (not current). | Header shows "Version: base" (not "v2"). |
| 7 | Open Analytics for a run executed with "v2". | Header shows "Version: v2". |

## Pass/Fail Criteria

**Pass:** Header shows correct format and executed version matching Run History.
**Fail:** Wrong format, or shows current editor version instead of executed version.
