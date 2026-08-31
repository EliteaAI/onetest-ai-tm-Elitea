---
id: ELITEA-2965
title: "ADO Work Item Text Search – Optional Filters Map to the Correct ADO Field, Only When Provided"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2965: ADO Work Item Text Search – Optional Filters Map to the Correct ADO Field, Only When Provided

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify each optional filter (`work_item_type`, `state`, `assigned_to`, `area_path`) maps to its correct underlying ADO field, and is only added to the request when explicitly provided.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- Work items exist covering a range of types, states, assignees, and area paths.

---

## Test Data

| Filter | Example value (as list) |
|--------|--------------------------|
| work_item_type | `["Bug"]` |
| state | `["Active"]` |
| assigned_to | `["<a known assignee display name>"]` |
| area_path | `["<a known area path>"]` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with only `query` set, no filters | Result set is unfiltered by type/state/assignee/area |
| 2 | Call with `work_item_type` set | Only that type appears in results |
| 3 | Call with `state` set | Only that state appears in results |
| 4 | Call with `assigned_to` set | Only items assigned to that person appear |
| 5 | Call with `area_path` set | Only items under that area path appear |

---

## Expected Final State

Each filter, applied individually, narrows results to exactly the corresponding ADO field value; omitted filters impose no restriction.

---

## Pass/Fail Criteria

**Pass:** Each filter maps to and restricts by its correct field, and is absent from the request when not provided.
**Fail:** A filter is ignored, maps to the wrong field, or is silently applied even when not provided.
