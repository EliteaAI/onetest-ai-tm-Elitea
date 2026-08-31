---
id: ELITEA-2988
title: "ADO Work Item Text Search – No Cross-Talk Between search_work_items (WIQL) and search_work_items_by_text in the Same Session"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, inconclusive]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2988: ADO Work Item Text Search – No Cross-Talk Between search_work_items (WIQL) and search_work_items_by_text in the Same Session

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify calling the WIQL-based `search_work_items` and the new `search_work_items_by_text` tool in the same agent/chat session does not cause either tool to affect the other's behavior, caching, or results. **Status: previously untested — not exercised in the same session during exploratory testing.**

---

## Preconditions

- ADO Board toolkit is configured with valid credentials, exposing both tools.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | In one session, call `search_work_items` with a WIQL query, record results | Baseline WIQL results recorded |
| 2 | In the same session, call `search_work_items_by_text` with an unrelated text query | Call succeeds independently |
| 3 | Re-call `search_work_items` with the same WIQL query as step 1 | Results identical to step 1 (unaffected by the intervening text search call) |
| 4 | Re-call `search_work_items_by_text` with a query that overlaps filter values used implicitly by WIQL (e.g. same `work_item_type`) | Results are correct and independent of the WIQL call's state |

---

## Expected Final State

The two tools operate fully independently within a shared session; neither leaks state or cached filters into the other.

---

## Pass/Fail Criteria

**Pass:** Results from each tool are identical/consistent regardless of interleaving with the other tool.
**Fail:** Calling one tool changes the other's results, errors, or behavior within the same session.
