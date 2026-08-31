---
id: ELITEA-2977
title: "ADO Work Item Text Search – On a Normal Page, next_skip Equals skip + top of the Call Just Made"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2977: ADO Work Item Text Search – On a Normal Page, next_skip Equals skip + top of the Call Just Made

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify that for a non-final page, `next_skip` in the response equals `skip + top` of the request that produced it.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A query matches more items than a single page can return.

---

## Test Data

| Call | skip | top |
|------|------|-----|
| 1 | 0 | 10 |
| 2 | 10 | 10 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with `skip=0`, `top=10` against a query with >20 matches | Response includes `next_skip=10` |
| 2 | Call with `skip=10`, `top=10` on the same query | Response includes `next_skip=20` |

---

## Expected Final State

`next_skip` consistently equals `skip + top` on every non-final page.

---

## Pass/Fail Criteria

**Pass:** `next_skip` = `skip + top` holds in both calls.
**Fail:** `next_skip` is off by any amount, or inconsistent between calls.
