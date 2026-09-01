---
id: ELITEA-3056
title: "Empty-String response_search Is Treated as No Search, Not an Error or Zero-Match"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3056: Empty-String response_search Is Treated as No Search

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm submitting `response_search=""` (empty string) or a whitespace-only string is treated as if the argument were not supplied at all — falling back to limit-only/full behavior — rather than erroring or matching zero items. Confirmed live during the follow-up checklist pass ("empty string → legacy fallback").

---

## Preconditions

- An OpenAPI toolkit configured against any operation with a JSON array response.

---

## Test Data

| Field | Value |
|-------|-------|
| `response_search` | `""` (empty string) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search=""` and no `response_limit`. | The full (or default-limited) response is returned as if `response_search` had not been supplied — not an error, not an empty-match result. |
| 2 | Repeat with a whitespace-only string (e.g. `"   "`). | Same fallback behavior. |

---

## Expected Final State

Empty/whitespace-only search strings are normalized to "no search" rather than triggering an error or a spurious zero-match result.

---

## Pass/Fail Criteria

**Pass:** Both empty and whitespace-only search strings fall back to unfiltered/limit-only behavior.
**Fail:** Either input raises an error or is treated as a zero-match search.
