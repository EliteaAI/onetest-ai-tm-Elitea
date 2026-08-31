---
id: ELITEA-2990
title: "ADO Work Item Text Search – Exact Boundary Pairs: top=50 vs 51 and skip=1000 vs 1001"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104, new]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2990: ADO Work Item Text Search – Exact Boundary Pairs: top=50 vs 51 and skip=1000 vs 1001

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Isolate ceiling correctness from rejection mechanism with discrete adjacent-value pairs, consolidating and sharpening [[ELITEA-2968]] and [[ELITEA-2969]] into single boundary-focused assertions.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Parameter | At ceiling (must succeed) | One above ceiling (must hard-error) |
|-----------|------------------------------|----------------------------------------|
| top | `50` | `51` |
| skip | `1000` | `1001` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `top=50` | Succeeds |
| 2 | Call with `top=51` | Hard tool error |
| 3 | Call with `skip=1000` | Succeeds |
| 4 | Call with `skip=1001` | Hard tool error |

---

## Expected Final State

The ceilings (50 for `top`, 1000 for `skip`) are exactly where behavior flips from success to hard error — no off-by-one drift in either direction.

---

## Pass/Fail Criteria

**Pass:** All four boundary calls behave exactly as specified.
**Fail:** Any boundary has shifted (e.g. `top=50` now errors, or `top=51` now succeeds).
