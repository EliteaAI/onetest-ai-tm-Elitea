---
id: ELITEA-2978
title: "ADO Work Item Text Search – Repeating next_skip as the Next skip Converges Without Loops or Gaps"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2978: ADO Work Item Text Search – Repeating next_skip as the Next skip Converges Without Loops or Gaps

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify that mechanically following the pagination chain (feeding each response's `next_skip` back in as the next call's `skip`) walks through the full result set exactly once, with no infinite loop, no repeated items across pages, and no skipped items.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A query matches enough items to span at least 3 pages at a chosen `top`.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `skip=0`, a fixed `top` (e.g. 10); collect result `id`s and note `next_skip` | Page 1 collected |
| 2 | Feed `next_skip` as `skip` in the next call, repeat until `next_skip` is absent | Terminates after ⌈total_count / top⌉ pages |
| 3 | Union all collected `id`s across every page | No duplicate `id` appears across pages; no gap — the union's size equals `total_count` |

---

## Expected Final State

The full result set is covered exactly once by mechanically walking `next_skip`, with no loop and no missing/duplicated items.

---

## Pass/Fail Criteria

**Pass:** Walking `next_skip` terminates, and the union of all pages has exactly `total_count` unique items.
**Fail:** The walk loops indefinitely (never omits `next_skip`), or the union has duplicates or is short of `total_count`.
