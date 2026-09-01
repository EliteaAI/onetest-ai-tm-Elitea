---
id: ELITEA-3069
title: "Oversized Single/Selected Result Triggers Progressive Truncation, Then content_too_large Fallback"
priority: medium
type: functional
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, api, new, needs-fixture]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3069: Oversized Single/Selected Result Triggers Progressive Truncation, Then content_too_large Fallback

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that when a single selected/matched item (or the fully filtered set) serializes to more than 50,000 characters, the tool first attempts progressive truncation, and if that's still insufficient, returns `status: "content_too_large"` rather than an unbounded/oversized payload or a crash. **Blocked during live exploration this session** — the user was unable to force a >50,000-character single result against the public APIs tried in the time available. Requires a constructed fixture (or a public API endpoint known to return a very large single object) to execute.

---

## Preconditions

- An OpenAPI toolkit configured against an operation capable of returning a single item whose serialized size exceeds 50,000 characters (e.g. a large nested object with many fields/sub-arrays).

---

## Test Data

| Field | Value |
|-------|-------|
| Fixture/endpoint | operation returning one item >50,000 serialized chars |
| `response_search`/`response_limit` | set such that exactly one (very large) item is selected |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call the tool such that the selected/matched result is the oversized item. | Call succeeds (no unhandled exception). |
| 2 | Inspect the response. | Either progressively truncated content is returned with truncation clearly indicated, or `status: "content_too_large"` is returned if truncation isn't sufficient. |
| 3 | Confirm no raw unbounded payload is ever returned. | Response size stays within the tool's documented bound in all cases. |

---

## Expected Final State

Oversized results are always degraded gracefully — truncated or explicitly flagged — never returned raw and unbounded.

---

## Pass/Fail Criteria

**Pass:** Truncation or `content_too_large` status behaves as documented; no unbounded payload or crash.
**Fail:** An oversized raw payload is returned without truncation/flagging, or the call errors unhandled.

---

## Blocked / Fixture Needed

Could not be forced via public APIs tried this session. Author a fixture spec/mock server (or find a suitable public API) returning a sufficiently large single item before executing.
