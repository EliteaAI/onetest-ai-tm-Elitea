---
id: ELITEA-3068
title: "Keyed Object-Map Response Is Selected and Returned as a Map, Not Flattened Into an Array"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, needs-fixture]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3068: Keyed Object-Map Response Is Selected and Returned as a Map

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that when the response collection is a keyed object map (e.g. `{ "US": {...}, "CA": {...}, "MX": {...} }`, ≥3 entries, all non-empty dicts, a common field present in ≥70% of entries — the runtime object-map heuristic), the tool correctly identifies it as `collection_kind: "object_map"` and returns the filtered/limited result still keyed by its original keys — not flattened into a plain array that discards the keys. **Blocked during live exploration this session** — no suitable public API returning this exact keyed-map shape was identified/tested. Requires a constructed fixture to execute.

---

## Preconditions

- An OpenAPI toolkit configured against an operation whose response is a keyed object map meeting the runtime heuristic (≥3 entries, all dict values, common field in ≥70%).

---

## Test Data

| Field | Value |
|-------|-------|
| Fixture/endpoint | keyed map, e.g. `{ "US": {"name": "United States", "population": ...}, "CA": {...}, "MX": {...} }` |
| `response_search` | term matching a subset of the entries' common field |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search` against the keyed-map endpoint. | Call succeeds. |
| 2 | Inspect `_elitea_response_selection.collection_kind`. | `"object_map"`. |
| 3 | Inspect the returned collection. | Still a keyed object (not an array) containing only the matching entries, each retaining its original key. |

---

## Expected Final State

Object-map responses are filtered while preserving their keyed structure.

---

## Pass/Fail Criteria

**Pass:** `collection_kind: "object_map"` and the filtered result remains a keyed map with original keys intact.
**Fail:** The map is flattened into an array (keys lost), or misclassified as `"array"`.

---

## Blocked / Fixture Needed

No public API tested this session exposed a qualifying keyed object-map response. Author a fixture spec/mock server before executing.
