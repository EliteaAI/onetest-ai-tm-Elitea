---
id: ELITEA-3059
title: "Zero-Match Search Query Returns Valid JSON With an Empty Collection, Not an Error"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3059: Zero-Match Search Query Returns Valid JSON With an Empty Collection

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm a `response_search` query matching zero items returns valid JSON with an empty collection and `matched_items: 0`/`returned_items: 0` in the metadata — not an error, and not the unfiltered full response. Confirmed live during manual exploration ("zero-match query" — clean empty result; follow-up "zero-match handling").

---

## Preconditions

- An OpenAPI toolkit configured against any operation with a searchable JSON response.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | a nonsense term guaranteed not to match (e.g. `"zzznonexistentqueryterm999"`) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with the nonsense query term. | Call succeeds (no error). |
| 2 | Inspect the response. | Valid JSON with an empty collection (e.g. `{"items": []}`) at the original collection path. |
| 3 | Inspect metadata. | `matched_items: 0`, `returned_items: 0`. |

---

## Expected Final State

Zero matches is a normal, well-formed outcome, not an error path.

---

## Pass/Fail Criteria

**Pass:** Empty but valid JSON collection with correct zero-count metadata.
**Fail:** An error is raised, or the full unfiltered response is returned instead.
