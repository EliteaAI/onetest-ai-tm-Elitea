---
id: ELITEA-2962
title: "ADO Work Item Text Search – Query Scopes to the Toolkit's Configured Project"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2962: ADO Work Item Text Search – Query Scopes to the Toolkit's Configured Project

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify calling `search_work_items_by_text` with only `query` set returns results scoped to the toolkit's configured ADO project, with no cross-project leakage.

---

## Preconditions

- ADO Board toolkit is configured against a single specific project.
- The ADO organization contains at least one other project with work items.

---

## Test Data

| Field | Value |
|-------|-------|
| query | A text term known to match work items in the configured project |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with only `query` set | Call succeeds |
| 2 | Inspect the `project` field on every returned result | Every result's project matches the toolkit's configured project |
| 3 | Confirm no result belongs to a different ADO project in the same org | No cross-project results present |

---

## Expected Final State

Results are strictly scoped to the toolkit's configured project.

---

## Pass/Fail Criteria

**Pass:** All returned results belong to the configured project only.
**Fail:** Any result belongs to a different project.
