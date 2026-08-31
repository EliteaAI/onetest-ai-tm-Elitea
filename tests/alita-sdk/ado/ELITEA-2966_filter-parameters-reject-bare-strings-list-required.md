---
id: ELITEA-2966
title: "ADO Work Item Text Search – Filter Parameters Reject a Bare String; a List Is Required (Known Limitation)"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, known-limitation]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2966: ADO Work Item Text Search – Filter Parameters Reject a Bare String; a List Is Required (Known Limitation)

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Confirm the currently-observed behavior: `work_item_type`, `state`, `assigned_to`, and `area_path` each reject a bare string value with a tool execution error — a single value must still be wrapped in a list. This is a known limitation, tracked here so a future fix (accepting bare strings) or regression (tightening further) is caught.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Filter | Bare-string value (expected to fail) | Equivalent list value (expected to succeed) |
|--------|----------------------------------------|-----------------------------------------------|
| work_item_type | `"Bug"` | `["Bug"]` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with `work_item_type="Bug"` (bare string) | Tool execution error is returned |
| 2 | Call again with `work_item_type=["Bug"]` (list) | Call succeeds normally |

---

## Expected Final State

A bare string is rejected; the equivalent single-item list succeeds — confirming the current (limited) contract.

---

## Pass/Fail Criteria

**Pass:** Bare string errors out; single-item list succeeds — matches documented known limitation.
**Fail:** Behavior has changed (e.g. bare string now silently succeeds without update to docs, or the list form has also stopped working).
