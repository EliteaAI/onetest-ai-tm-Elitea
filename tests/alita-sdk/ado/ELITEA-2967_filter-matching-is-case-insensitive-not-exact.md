---
id: ELITEA-2967
title: "ADO Work Item Text Search – Filter-Value Matching Is Case-Insensitive, Not Exact (Known Behavior)"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, known-limitation]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2967: ADO Work Item Text Search – Filter-Value Matching Is Case-Insensitive, Not Exact (Known Behavior)

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Confirm the currently-observed behavior: filter values for `work_item_type` and `state` match case-insensitively (e.g. `"issue"` behaves identically to `"Issue"`), rather than requiring an exact case-sensitive match.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- Work items exist of a known type/state with standard ADO casing (e.g. `Issue`, `To Do`).

---

## Test Data

| Filter | Canonical-case value | Deliberately-mismatched-case value |
|--------|------------------------|--------------------------------------|
| work_item_type | `["Issue"]` | `["issue"]` |
| state | `["To Do"]` | `["to do"]` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `work_item_type=["Issue"]`, record `total_count` | Baseline count A |
| 2 | Call with `work_item_type=["issue"]`, record `total_count` | Count B equals count A |
| 3 | Repeat steps 1–2 for `state` with `["To Do"]` vs `["to do"]` | Counts match in both cases |

---

## Expected Final State

Case-mismatched filter values return identical results to their canonical-case counterparts.

---

## Pass/Fail Criteria

**Pass:** Result counts are identical regardless of casing — matches documented known behavior.
**Fail:** Casing now affects the result set (i.e. matching became case-sensitive without a corresponding doc/behavior update).
