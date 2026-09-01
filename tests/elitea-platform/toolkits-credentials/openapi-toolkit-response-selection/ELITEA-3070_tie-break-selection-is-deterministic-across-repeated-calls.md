---
id: ELITEA-3070
title: "Candidate Tie-Break Selection Is Deterministic Across Repeated Calls"
priority: low
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, needs-fixture]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3070: Candidate Tie-Break Selection Is Deterministic Across Repeated Calls

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Low · **Type:** Functional

**Objective:** Confirm that when multiple collection candidates tie through the full tie-break cascade (schema-declared → BM25 relevance within tolerance → common-key priority → shorter path → ≥2x larger collection), the same candidate is chosen consistently across repeated identical calls — not a nondeterministic/random choice that could vary between calls or environments. **Blocked during live exploration this session** — no suitable public API produced a genuine multi-candidate tie within tolerance in the time available. Requires a constructed fixture with deliberately tied candidates to execute.

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning a response with two or more collection candidates that tie through the documented cascade (equal BM25 relevance within `rel_tol=1e-9`/`abs_tol=1e-12`, no differing common-key priority, equal path length, neither ≥2x larger).

---

## Test Data

| Field | Value |
|-------|-------|
| Fixture/endpoint | response with 2+ genuinely tied candidates |
| `response_search` | query producing equal relevance across the tied candidates |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with the same request 5 times against the tied-candidate fixture. | All 5 calls succeed. |
| 2 | Compare `collection_path` in `_elitea_response_selection` across all 5 responses. | Identical `collection_path` every time. |
| 3 | Compare returned content across all 5 responses. | Identical content every time (same items, same order). |

---

## Expected Final State

Tie-break resolution is stable and reproducible, not a source of flaky/nondeterministic behavior.

---

## Pass/Fail Criteria

**Pass:** All 5 repeated calls select the identical candidate and return identical content.
**Fail:** Any call selects a different candidate or returns differently-ordered/different content than the others.

---

## Blocked / Fixture Needed

No public API tested this session produced a genuine tie within tolerance. Author a fixture spec/mock server with deliberately tied candidates before executing.
