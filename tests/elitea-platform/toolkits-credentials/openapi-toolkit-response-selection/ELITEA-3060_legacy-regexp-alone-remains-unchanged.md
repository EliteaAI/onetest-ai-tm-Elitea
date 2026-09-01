---
id: ELITEA-3060
title: "Legacy regexp Field Used Alone Remains Behaviorally Unchanged"
priority: critical
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, regression]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3060: Legacy regexp Field Used Alone Remains Behaviorally Unchanged

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm the pre-existing `regexp` field, when used alone (no `response_search`/`response_limit`), preserves its legacy `re.sub()`-based text-removal behavior byte-for-byte, unaffected by this feature's introduction. Confirmed live during manual exploration ("legacy regexp alone" — backward compatible).

---

## Preconditions

- An OpenAPI toolkit operation and `regexp` pattern already known to work correctly before this feature shipped.

---

## Test Data

| Field | Value |
|-------|-------|
| `regexp` | a previously-validated pattern for this operation |
| `response_search` | not supplied |
| `response_limit` | not supplied |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with only the `regexp` pattern set. | Call succeeds. |
| 2 | Compare output against the pre-feature baseline for the same call. | Output is identical — the matched text is removed exactly as before, no new metadata or wrapper added. |

---

## Expected Final State

`regexp`-alone behavior is fully preserved.

---

## Pass/Fail Criteria

**Pass:** Output matches the legacy baseline exactly.
**Fail:** Any behavioral difference is observed, including unexpected metadata injection.
