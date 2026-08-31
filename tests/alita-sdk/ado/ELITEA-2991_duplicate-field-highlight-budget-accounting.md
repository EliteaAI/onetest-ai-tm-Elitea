---
id: ELITEA-2991
title: "ADO Work Item Text Search – Duplicate-Field Highlight Budget Accounting (Suspected Bug, Needs Isolation)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, new, suspected-bug]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2991: ADO Work Item Text Search – Duplicate-Field Highlight Budget Accounting (Suspected Bug, Needs Isolation)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Determine whether two separate highlight snippets for the *same* field name on one result both count against the documented 3-fields-per-result highlight budget, or whether they're incorrectly double-counted/under-counted. This was noticed incidentally during exploratory testing and has not yet been formally isolated or filed as a bug.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A work item is identified/constructed where the search term appears more than once within a single field (e.g. two separate matches inside a long description), such that the ADO Search API may return multiple highlight fragments for that one field.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Identify or construct a work item + query where a single field yields multiple highlight fragments | Candidate confirmed |
| 2 | Call `search_work_items_by_text` with `include_highlights=true` against that query | Call succeeds |
| 3 | Inspect that result's `highlights` object structure | Determine: is it one entry per field (fragments merged/concatenated) or one entry per fragment (same field name appearing twice)? |
| 4 | If the same field name appears twice, check whether the 3-field cap ([[ELITEA-2983]]) is still enforced correctly (i.e. counts unique fields, not fragments) | Cap correctly reflects distinct fields, not fragment count |

---

## Expected Final State

The highlight budget should be defined and enforced per distinct field name — multiple fragments within one field should not silently consume two slots of the 3-field cap (or, if the design intends fragment-level counting, that should be documented explicitly).

---

## Pass/Fail Criteria

**Pass:** Multi-fragment matches within a single field are merged into one highlight entry, and the 3-field cap counts distinct fields correctly.
**Fail:** A single field's multiple fragments consume more than one slot of the 3-field cap, silently reducing the effective number of distinct fields shown — confirm and file as a bug if reproduced.
