---
id: ELITEA-2973
title: "ADO Work Item Text Search – id Is Numeric, url Follows the Edit-Link Pattern, assigned_to Omitted When Absent"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2973: ADO Work Item Text Search – id Is Numeric, url Follows the Edit-Link Pattern, assigned_to Omitted When Absent

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify per-result field shape: `id` is numeric when the underlying ADO ID is numeric, `url` follows the `_workitems/edit/{id}` pattern, and `assigned_to` is omitted (not `null`/empty string) when the work item has no assignee.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- At least one matching work item has no assignee.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with a query matching several work items, including at least one unassigned item | Call succeeds |
| 2 | Inspect `id` on each result | `id` is a numeric type, matching the work item's ADO ID |
| 3 | Inspect `url` on each result | `url` matches the `.../_workitems/edit/{id}` pattern with the correct `{id}` |
| 4 | Inspect the unassigned work item's result object | `assigned_to` key is entirely absent, not `null` or `""` |

---

## Expected Final State

Field types and shapes match the documented contract exactly, including the omission rule for `assigned_to`.

---

## Pass/Fail Criteria

**Pass:** `id` is numeric, `url` matches the pattern, and `assigned_to` is omitted when absent.
**Fail:** `id` is a string, `url` is malformed/incorrect, or `assigned_to` appears as `null`/empty for an unassigned item.
