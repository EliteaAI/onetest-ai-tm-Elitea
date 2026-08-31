---
id: ELITEA-2982
title: "ADO Work Item Text Search – Highlights Are Capped at the First 5 Hit-Bearing Results, With a Withheld-Count Warning"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2982: ADO Work Item Text Search – Highlights Are Capped at the First 5 Hit-Bearing Results, With a Withheld-Count Warning

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that with `include_highlights=true` and more than 5 hit-bearing results, only the first 5 carry `highlights`, and a warning states how many further results had their highlights withheld.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A query matches more than 5 hit-bearing results (returned within `top`).

---

## Test Data

| Field | Value |
|-------|-------|
| query | A term matching at least 7 work items, with `top` set to include all of them |
| include_highlights | `true` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `include_highlights=true` against the query above | Call succeeds |
| 2 | Count results carrying a `highlights` key | Exactly the first 5 hit-bearing results carry it |
| 3 | Inspect the response for a "further results withheld" warning | Warning present, stating the correct withheld count |

---

## Expected Final State

At most 5 results ever carry highlights per response; withholding beyond that is explicitly communicated.

---

## Pass/Fail Criteria

**Pass:** Exactly 5 (or fewer, if fewer hit-bearing results exist) carry highlights, with an accurate withheld-count warning when applicable.
**Fail:** More than 5 results carry highlights, or the withheld-count warning is missing/incorrect.
