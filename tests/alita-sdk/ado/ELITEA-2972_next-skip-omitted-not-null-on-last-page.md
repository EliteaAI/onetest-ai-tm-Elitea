---
id: ELITEA-2972
title: "ADO Work Item Text Search – next_skip Is Omitted Entirely (Never null) Once There Is No Further Page"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2972: ADO Work Item Text Search – next_skip Is Omitted Entirely (Never null) Once There Is No Further Page

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify that on the final page of results, the `next_skip` key is absent from the response object entirely, rather than present with a `null` value.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.
- A query is known to match fewer results than the requested `top`, or paging has reached the last page.

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call with a query/`top` combination where `returned < top` (i.e. no further page exists) | Response does not contain a `next_skip` key at all |
| 2 | Programmatically check `"next_skip" in response` (or equivalent key-presence check, not just truthiness) | Key is absent, not present-and-null |

---

## Expected Final State

`next_skip` is a key that only exists when more results remain; it is never emitted as `null`.

---

## Pass/Fail Criteria

**Pass:** `next_skip` key is fully absent on the last page.
**Fail:** `next_skip` is present with value `null` (or any other placeholder) instead of being omitted.
