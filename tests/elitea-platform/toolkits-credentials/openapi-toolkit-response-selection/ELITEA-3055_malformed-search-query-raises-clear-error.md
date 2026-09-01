---
id: ELITEA-3055
title: "Malformed response_search Query Raises a Clear Error, Not Silent Misbehavior"
priority: high
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3055: Malformed response_search Query Raises a Clear Error, Not Silent Misbehavior

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Functional

**Objective:** Confirm a malformed `response_search` query — an unterminated quote (`"unterminated`) or a bare `-` with nothing after it — raises a clear error (`ResponseSelectionError`) rather than silently ignoring the malformed part, matching the wrong items, or crashing with an unhandled exception. Confirmed live during the follow-up checklist pass ("malformed queries").

---

## Preconditions

- An OpenAPI toolkit configured against any operation with a searchable JSON response.

---

## Test Data

| Field | Value |
|-------|-------|
| Malformed query A | `"unterminated` (unterminated quote) |
| Malformed query B | `-` (bare exclusion marker, no term) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search="\"unterminated"`. | A clear, structured error is returned — not a 500/unhandled exception, and not a silent match against the literal text. |
| 2 | Call the tool with `response_search="-"`. | A clear, structured error is returned in the same manner. |

---

## Expected Final State

Malformed search syntax fails loudly and predictably rather than degrading silently.

---

## Pass/Fail Criteria

**Pass:** Both malformed inputs produce a clear, structured error.
**Fail:** Either input crashes unhandled, silently matches unexpected content, or is otherwise mishandled without a clear error.
