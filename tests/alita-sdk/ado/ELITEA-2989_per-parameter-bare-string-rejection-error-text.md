---
id: ELITEA-2989
title: "ADO Work Item Text Search – Per-Parameter Bare-String Rejection Error Text (work_item_type/state/assigned_to/area_path)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, new]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2989: ADO Work Item Text Search – Per-Parameter Bare-String Rejection Error Text (work_item_type/state/assigned_to/area_path)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Individually run each of the four filter parameters as a bare string (not a list) and capture the exact tool error text for each, to precisely document the known bare-string-rejection limitation ([[ELITEA-2966]]) per parameter rather than as one general claim.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Parameter | Bare-string value |
|-----------|---------------------|
| work_item_type | `"Issue"` |
| state | `"Active"` |
| assigned_to | `"<a known assignee display name>"` |
| area_path | `"<a known area path>"` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `work_item_type="Issue"` (bare string) | Tool error returned; record exact error text |
| 2 | Call with `state="Active"` (bare string) | Tool error returned; record exact error text |
| 3 | Call with `assigned_to="<name>"` (bare string) | Tool error returned; record exact error text |
| 4 | Call with `area_path="<path>"` (bare string) | Tool error returned; record exact error text |

---

## Expected Final State

All four parameters independently reject bare strings, each with a specific, informative error message (ideally naming the offending parameter and stating a list is required).

---

## Pass/Fail Criteria

**Pass:** All four calls error out, and each error message clearly identifies the parameter and the list requirement.
**Fail:** Any parameter's error message is generic/unhelpful, or any parameter unexpectedly accepts the bare string.
