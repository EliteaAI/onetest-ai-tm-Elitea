---
id: ELITEA-4128
title: "search_work_items returns the work item Type, and returns the WIQL SELECT columns when no fields are given"
priority: high
type: functional
module: ado
status: ready
execution_type: manual
tags: [sdk, ado, toolkit, work-items, wiql, issue:7141, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7141"]
---

# ELITEA-4128: search_work_items returns the work item Type, and returns the WIQL SELECT columns when no fields are given

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify that the WIQL-based `search_work_items` returns `System.WorkItemType`, both by default and when it's requested in `fields`. When `fields` isn't given, the result must have exactly the columns of the WIQL `SELECT`. When the `SELECT` gives nothing usable, the tool falls back to the default list. Explicit `fields` always take priority over the `SELECT`.

---

## Preconditions

- An ADO Boards / Work Items toolkit is configured with valid credentials for project **P**.
- P has at least one **Bug** and one **User Story** (or Task) in state Active, with known IDs **B1** and **U1**.
- B1 is **unassigned** (needed for step 8).
- You can run the toolkit's tools directly (toolkit Test / tool runner), so you see the raw tool output.

---

## Test Data

| Name | Query |
|------|-------|
| Q-ID | `SELECT [System.Id] FROM WorkItems WHERE [System.Id] IN (B1, U1)` |
| Q-COLS | `SELECT [System.Id], [System.Title], [System.WorkItemType] FROM WorkItems WHERE [System.Id] IN (B1, U1)` |
| Q-CUSTOM | `SELECT [System.Id], [Microsoft.VSTS.Common.Priority] FROM WorkItems WHERE [System.Id] IN (B1, U1)` |
| Q-STAR | `SELECT * FROM WorkItems WHERE [System.Id] IN (B1, U1)` |

Default fields: `System.Title`, `System.State`, `System.AssignedTo`, `System.WorkItemType`, `System.CreatedDate`, `System.ChangedDate`.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run `search_work_items` with **Q-ID** and no `fields`. | 2 items. Each has `id`, `url` and the **6 default fields**. `System.WorkItemType` is "Bug" for B1 and "User Story" (or "Task") for U1. |
| 2 | Run Q-ID with `fields=["System.Title", "System.WorkItemType"]`. | Each item has exactly `id`, `url`, `System.Title` and `System.WorkItemType`, and the Type is correct. |
| 3 | Run **Q-COLS** with no `fields`. | Each item has exactly `id`, `url`, `System.Title` and `System.WorkItemType`. There is no `System.State` or other default field. |
| 4 | Run Q-COLS with `fields=["System.State"]`. | Explicit `fields` win. Each item has `id`, `url` and `System.State` only. |
| 5 | Run **Q-CUSTOM** with no `fields`. | Each item has `Microsoft.VSTS.Common.Priority` with its value. Custom and non-System fields are kept. |
| 6 | Run **Q-STAR** with no `fields`. | No error. Each item has `id` and `url`. Record which fields come back: the ADO expansion of `*` or the default list. Either is acceptable. |
| 7 | Run Q-ID with `fields=[]`. | The 6 default fields are returned. The call doesn't fail with an empty field list. |
| 8 | Run Q-ID with `fields=["System.AssignedTo", "System.WorkItemType"]`. | For the unassigned B1, `System.AssignedTo` is `N/A`, and `System.WorkItemType` is still "Bug". |
| 9 | Run a query that matches nothing, e.g. `... WHERE [System.Id] = 0`. | The output is `No work items found.` (unchanged). |
| 10 | Open the tool description and the `query` / `fields` argument descriptions in the toolkit. | They say that the `SELECT` columns are returned, that `fields` overrides them, and they list the defaults, including `System.WorkItemType`. |

---

## Expected Final State

Type is always available from `search_work_items`, and the output follows the `SELECT` unless `fields` overrides it.

---

## Pass/Fail Criteria

**Pass:**
- `System.WorkItemType` is returned with the right value in steps 1, 2, 3 and 8.
- The `SELECT` columns decide the output when `fields` isn't given (steps 3, 5). `fields` overrides them (step 4).
- The fallback to the defaults works (steps 1, 7). Steps 6 and 9 don't error.

**Fail:**
- Type is missing when it's in the defaults, in `fields` or in the `SELECT`.
- The output ignores the `SELECT` columns, or ignores explicit `fields`.
- `fields=[]` or `SELECT *` causes an error.
