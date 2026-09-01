---
id: ELITEA-3067
title: "Response Envelope Siblings (count, next, etc.) Are Preserved Around the Selected Collection"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, needs-fixture]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3067: Response Envelope Siblings Are Preserved Around the Selected Collection

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that when an operation's response is an envelope object with the collection as one field among siblings (e.g. `{ "count": 137, "items": [...], "next": "cursor-abc" }`), applying `response_search`/`response_limit` replaces only the collection field's contents — sibling fields like `count`/`next` remain present and untouched (not stripped, not recomputed to match the filtered subset). **Blocked during live exploration this session** — no suitable public API endpoint with this exact envelope shape was found within the time available. Requires a constructed fixture or a different public API to execute.

---

## Preconditions

- An OpenAPI toolkit configured against an operation whose response is an envelope object containing both a collection field and non-collection sibling fields (e.g. pagination metadata).

---

## Test Data

| Field | Value |
|-------|-------|
| Fixture/endpoint | envelope shape `{ count, items, next }` or equivalent |
| `response_search` | a term matching a subset of `items` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search` set against the envelope endpoint. | Call succeeds. |
| 2 | Inspect the top-level response shape. | Sibling fields (`count`, `next`, etc.) are present and equal to their original upstream values — not removed, not recalculated against the filtered subset. |
| 3 | Inspect the collection field itself. | Contains only the filtered/ranked subset, per `_elitea_response_selection` metadata (`matched_items`, `returned_items`). |

---

## Expected Final State

The envelope structure is preserved; only the collection contents are replaced by the selection result.

---

## Pass/Fail Criteria

**Pass:** Sibling envelope fields are untouched; only the collection field reflects filtering.
**Fail:** Sibling fields are dropped, altered, or incorrectly recomputed based on the filtered subset.

---

## Blocked / Fixture Needed

No public API tested this session returned this exact envelope shape for a filterable collection. Author a fixture spec/mock server, or identify a suitable public API, before executing.
