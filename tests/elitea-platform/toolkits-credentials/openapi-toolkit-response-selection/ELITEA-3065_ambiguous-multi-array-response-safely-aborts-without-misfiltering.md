---
id: ELITEA-3065
title: "Ambiguous Multi-Array Nested Response Safely Aborts Instead of Silently Misfiltering"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, edge-case]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3065: Ambiguous Multi-Array Nested Response Safely Aborts

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** **New edge case discovered during live exploration** (PokeAPI): a response containing multiple similarly-plausible nested array candidates, with no schema hint or common-envelope-key resolving the ambiguity, causes the tool to safely abort with `status: "ambiguous_collection"` rather than silently guessing and misfiltering. Confirm this is genuinely a safe abort (structured guidance, no silent wrong-data return), and flag to the maintainers as a UX question worth a design decision: should this default to the largest/most relevant array instead of aborting, or is abort-and-ask the intended behavior?

---

## Preconditions

- An OpenAPI toolkit configured against an operation known to return multiple plausible array candidates with no schema-declared or common-key resolution (e.g. a public API like PokeAPI on an endpoint with several sibling arrays).

---

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | one with 2+ ambiguous array candidates (e.g. PokeAPI Pikachu resource) |
| `response_search` | any valid query |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search` against the ambiguous endpoint. | Call succeeds (no crash). |
| 2 | Inspect the response. | `status: "ambiguous_collection"`, `candidate_paths` (capped at 20), `candidate_count`, `data: null`. |
| 3 | Confirm no partial/wrong-array data is silently returned instead. | No misleading data is present — the response is purely the ambiguity-guidance structure. |

---

## Expected Final State

Ambiguous cases fail safely with actionable guidance rather than guessing incorrectly.

---

## Pass/Fail Criteria

**Pass:** `ambiguous_collection` status with correct guidance fields, `data: null`, no silent misfiltered data.
**Fail:** The tool silently picks a wrong array and returns misfiltered data instead of surfacing the ambiguity.

---

## Notes

Not itself a defect — flagged as a product/UX question for the #6105 maintainers on whether "abort and list candidates" is preferable to "default to best-guess candidate" for this class of response.
