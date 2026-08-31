---
id: ELITEA-2983
title: "ADO Work Item Text Search – Each Highlighted Result Carries at Most 3 Matched Fields"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2983: ADO Work Item Text Search – Each Highlighted Result Carries at Most 3 Matched Fields

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that no single result's `highlights` object contains more than 3 field entries, even if the underlying work item matched on more fields.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- At least one matching work item has the search term present in more than 3 distinct fields (e.g. title, description, and multiple custom fields).

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `include_highlights=true` against a query matching a work item with hits in >3 fields | Call succeeds |
| 2 | Count the number of field entries in that result's `highlights` object | At most 3 |

---

## Expected Final State

The 3-field cap is enforced per result regardless of how many fields actually matched.

---

## Pass/Fail Criteria

**Pass:** No result's `highlights` object exceeds 3 field entries.
**Fail:** Any result's `highlights` object contains more than 3 field entries.
