---
id: ELITEA-2979
title: "ADO Work Item Text Search – A Filter Value Matching Nothing Surfaces a Standard, Work-Item-Specific Warning"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2979: ADO Work Item Text Search – A Filter Value Matching Nothing Surfaces a Standard, Work-Item-Specific Warning

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a filter value doesn't exist anywhere in the search index (the Azure DevOps Search API's infoCode-15-style condition), the tool surfaces a clear, work-item-specific warning rather than a silent empty result or a raw/opaque passthrough error.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Field | Value |
|-------|-------|
| area_path | A value guaranteed not to exist in the project, e.g. `"Nonexistent\\Area\\Path\\Zzz"` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with `query` set and `area_path` set to the nonexistent value | Call succeeds (does not hard-error) |
| 2 | Inspect the response for a warning field | A clear, work-item-specific warning is present explaining the filter value wasn't recognized |
| 3 | Confirm `total_count=0` | Result set is empty, consistent with the warning |

---

## Expected Final State

The nonexistent filter value produces a clear, actionable warning alongside an empty result set.

---

## Pass/Fail Criteria

**Pass:** A specific, human-readable warning about the unrecognized filter value is present.
**Fail:** No warning is surfaced, or the warning is generic/unrelated to the actual cause.
