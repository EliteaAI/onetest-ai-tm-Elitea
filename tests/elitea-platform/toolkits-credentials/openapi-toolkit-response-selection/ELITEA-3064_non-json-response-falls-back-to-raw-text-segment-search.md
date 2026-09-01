---
id: ELITEA-3064
title: "Non-JSON Response Falls Back to Raw-Text Segment Search"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3064: Non-JSON Response Falls Back to Raw-Text Segment Search

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm calling an operation whose response is not JSON (e.g. XML) with `response_search` supplied falls back to a bounded paragraph/line-based BM25 search over the raw text, with metadata showing `format: "text"`, `collection_path: "$segments"`, `collection_kind: "segments"`. Confirmed live during manual exploration (httpbin `/xml` — raw-text fallback confirmed).

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning a non-JSON body (e.g. `httpbin.org/xml` or equivalent).

---

## Test Data

| Field | Value |
|-------|-------|
| Endpoint | returns XML (non-JSON) body |
| `response_search` | a term present in the XML text |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool against the XML endpoint with `response_search` set. | Call succeeds (no JSON-parse error surfaced to the caller). |
| 2 | Inspect the metadata. | `format: "text"`, `collection_path: "$segments"`, `collection_kind: "segments"`. |
| 3 | Inspect the returned content. | Relevant paragraph/line segments containing the query term are returned, ranked by relevance. |

---

## Expected Final State

Non-JSON responses degrade gracefully into text-segment search rather than failing outright.

---

## Pass/Fail Criteria

**Pass:** Correct text-mode metadata and relevant segment(s) returned.
**Fail:** An error is raised for the non-JSON body, or the fallback metadata/format is incorrect.
