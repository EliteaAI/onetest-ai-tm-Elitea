---
id: ELITEA-2981
title: "ADO Work Item Text Search – include_highlights Defaults to Off; No highlights Key on Any Result by Default"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2981: ADO Work Item Text Search – include_highlights Defaults to Off; No highlights Key on Any Result by Default

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when `include_highlights` is omitted, no result carries a `highlights` key at all.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with `query` set and `include_highlights` omitted | Call succeeds |
| 2 | Inspect every result object for a `highlights` key | Key is absent on every result |

---

## Expected Final State

Highlights are strictly opt-in; omitting the flag never adds any highlight-related payload.

---

## Pass/Fail Criteria

**Pass:** No result has a `highlights` key when `include_highlights` is omitted.
**Fail:** Any result carries a `highlights` key (even empty) without the flag being set.
