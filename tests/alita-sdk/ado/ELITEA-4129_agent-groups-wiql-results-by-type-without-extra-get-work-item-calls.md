---
id: ELITEA-4129
title: "An agent groups WIQL search results by Type without extra get_work_item calls, and text search / get_work_item are unchanged"
priority: medium
type: functional
module: ado
status: ready
execution_type: manual
tags: [sdk, ado, toolkit, work-items, wiql, agents, issue:7141, r-2.0.8]
requirements: ["EliteaAI/elitea_issues#7141"]
---

# ELITEA-4129: An agent groups WIQL search results by Type without extra get_work_item calls, and text search / get_work_item are unchanged

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the user-facing scenario from elitea_support#1435. An agent that uses WIQL search can report each work item's Type straight from the search result, without calling `get_work_item` for every item. Also verify that `search_work_items_by_text` and `get_work_item` behave as before.

---

## Preconditions

- An agent **A** with the ADO Boards / Work Items toolkit, with only `search_work_items`, `get_work_item` and `search_work_items_by_text` enabled.
- Project P has at least 3 Active work items of at least 2 different Types (e.g. Bug and User Story).
- Chat shows tool calls, so you can count them.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In chat with A: "Using a WIQL query, find all Active work items in project P and list them grouped by work item type." | A calls `search_work_items` **once** and calls `get_work_item` **0** times. The answer groups the items by their real Types. Check the Types against ADO. |
| 2 | Expand the `search_work_items` call. | The tool output has `System.WorkItemType` for each item. If A wrote a `SELECT` that names columns, the output has those columns. |
| 3 | "Run this exact WIQL and show the result as a table: `SELECT [System.Id], [System.Title], [System.WorkItemType] FROM WorkItems WHERE [System.State] = 'Active'`" | The table has ID, Title and Type columns, with correct values. The tool output has no extra default fields. |
| 4 | "Search work items by text for '<a word from one of the titles>'." | `search_work_items_by_text` returns results with `type`, the same as before the fix. |
| 5 | "Get work item <id> with all its fields." | `get_work_item` with no `fields` returns all fields, including `System.WorkItemType`, the same as before the fix. |

---

## Expected Final State

The agent gets the Type from one WIQL search. The other two tools are unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Steps 1 to 3 give the correct Types without extra `get_work_item` calls per item.
- Steps 4 and 5 behave as before.

**Fail:**
- The search output has no Type, or the agent has to call `get_work_item` for each item to find it.
- The Types reported in the answer are wrong.
- The output of `search_work_items_by_text` or `get_work_item` changed.
