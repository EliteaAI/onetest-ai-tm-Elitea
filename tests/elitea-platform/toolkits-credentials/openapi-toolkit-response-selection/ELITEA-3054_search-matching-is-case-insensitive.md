---
id: ELITEA-3054
title: "response_search Matching Is Case-Insensitive"
priority: low
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3054: response_search Matching Is Case-Insensitive

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Low · **Type:** Functional

**Objective:** Confirm search matching is case-insensitive — a query in one case matches data written in a different case. Confirmed live during the follow-up checklist pass ("case-insensitivity").

---

## Preconditions

- An OpenAPI toolkit configured against an operation with response text containing a term in a specific case (e.g. `North America`).

---

## Test Data

| Field | Value |
|-------|-------|
| Data contains | `North America` |
| Query | `NORTH AMERICA` |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_search="NORTH AMERICA"` against data containing `North America`. | The item is matched despite the casing difference. |

---

## Expected Final State

Query casing has no effect on match outcome.

---

## Pass/Fail Criteria

**Pass:** The item matches regardless of casing difference between query and data.
**Fail:** The item is missed due to a casing mismatch.
