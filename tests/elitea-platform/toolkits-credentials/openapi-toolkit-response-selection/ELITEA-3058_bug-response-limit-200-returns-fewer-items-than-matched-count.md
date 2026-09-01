---
id: ELITEA-3058
title: "[BUG REPRO] response_limit=200 Returned Only 10 Items Despite matched_items:100"
priority: high
type: bug
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, bug, needs-reproduction]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3058: [BUG REPRO] response_limit=200 Returned Only 10 Items Despite matched_items:100

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** High · **Type:** Bug

**Objective:** During manual exploration, calling with `response_limit=200` against a dataset with `matched_items: 100` returned only **10** items instead of the expected up-to-100 (bounded by the smaller of `matched_items` and `response_limit`). This is inconsistent with `response_limit=3` behaving correctly in an earlier call against the same class of data. **This has not yet been confirmed as reliably reproducible** — this test case exists to systematically re-verify it and, if confirmed, capture enough detail (exact request, exact response, dataset) to file an SDK bug against PR #556's `select_response_content()` / limit-application logic.

---

## Preconditions

- An OpenAPI toolkit configured against an operation returning 100+ items (the same class of API/dataset used in the original observation, e.g. a large flat-array API such as the VSCode issues API used earlier in this exploration).

---

## Test Data

| Field | Value |
|-------|-------|
| `response_limit` | `200` |
| Dataset | one with 100+ matching items (`matched_items` expected ≈ 100) |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool with `response_limit=200` (no `response_search`) against a dataset with 100+ items. | `returned_items` should equal `min(matched_items, 200)` — expect ~100 items returned, matching `matched_items`. |
| 2 | Repeat the same call 2–3 more times to check for consistency. | Result count should be stable across repeated identical calls. |
| 3 | Repeat step 1 with `response_limit=3` on the same dataset as a control. | Confirm `response_limit=3` still correctly returns exactly 3 items (as previously observed working). |
| 4 | If step 1 still returns fewer than `min(matched_items, response_limit)` (e.g. exactly 10), capture the full request/response and file/attach to an SDK bug against `elitea_sdk/tools/openapi/response_selection.py`. | Bug is reproducible and documented with exact repro data. |

---

## Expected Final State

Either the anomaly does not reproduce (transient/environment issue, close as not-a-bug), or it reproduces consistently and is filed as a confirmed SDK defect in the limit-application path.

---

## Pass/Fail Criteria

**Pass:** `response_limit=200` returns `min(matched_items, 200)` items consistently across repeated calls.
**Fail:** `response_limit=200` returns fewer items than `min(matched_items, 200)` (e.g. capped at 10) — confirms the observed anomaly as a real defect.
