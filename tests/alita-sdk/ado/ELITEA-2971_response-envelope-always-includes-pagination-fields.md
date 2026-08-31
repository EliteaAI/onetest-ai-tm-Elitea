---
id: ELITEA-2971
title: "ADO Work Item Text Search – Response Envelope Always Includes total_count/returned/skip/truncated"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2971: ADO Work Item Text Search – Response Envelope Always Includes total_count/returned/skip/truncated

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify every response — including empty and single-page results — includes `total_count`, `returned`, `skip`, and `truncated`.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a query that matches nothing | Response includes `total_count=0`, `returned=0`, `skip=0`, `truncated=false` |
| 2 | Call with a query that matches a small number of items (fewer than `top`) | Response includes all four envelope fields with correct values |
| 3 | Call with a query that matches more items than `top` | Response includes all four envelope fields, `truncated=true` |

---

## Expected Final State

`total_count`, `returned`, `skip`, and `truncated` are present on every response shape (empty, partial, and truncated).

---

## Pass/Fail Criteria

**Pass:** All four envelope fields are present and correctly valued in every case.
**Fail:** Any of the four fields is missing, mistyped, or incorrect in any case.
