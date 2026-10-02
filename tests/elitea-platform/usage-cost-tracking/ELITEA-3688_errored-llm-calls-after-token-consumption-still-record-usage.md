---
id: ELITEA-3688
title: "A 4xx/5xx provider response after input tokens were consumed still produces a usage_event row with is_error=true and real tokens"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, error-handling, llm]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6574"]
---

# ELITEA-3688: A 4xx/5xx provider response after input tokens were consumed still produces a usage_event row with is_error=true and real tokens

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a provider returns a 4xx/5xx response **after** it has already consumed input tokens, a `usage_event` row is still produced with `is_error=true` and the real (non-zero) token counts. This is explicit #6571 scope and a named #6574 regression fix — a prior defect caused errored calls to contribute zero tokens/cost; reproducing that here is a live regression, not expected behavior.

---

## Preconditions

- Logged in to {{base_url}}.
- Ability to trigger an LLM call (chat, Build/Edit-with-AI, or agent run) against a model/endpoint that can be forced to fail **after** accepting the request (e.g. a request that is valid enough to be dispatched but fails downstream — oversized/invalid completion params, provider-side rate limit after acceptance, etc., depending on what's reproducible in the test environment).

---

## Test Data

| Field | Value |
|-------|-------|
| Failure trigger | Any reproducible way to get a 4xx/5xx **after** the provider accepted the request (environment-dependent) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger an LLM call that is accepted by the provider but then fails with a 4xx/5xx. | Call fails and is surfaced as an error in the UI. |
| 2 | Check `usage_event`/Analytics for a row corresponding to this call. | A row **is** present (not missing). |
| 3 | Inspect `is_error` on the row. | `is_error=true`. |
| 4 | Inspect the token counts on the row. | Real, non-zero input token counts are recorded (matching what was actually sent) — not a $0/0-token row. |

---

## Expected Final State

The errored-but-provider-billed call produces a complete `usage_event` row with `is_error=true` and real token counts — never a silent $0/0-token row.

---

## Pass/Fail Criteria

**Pass:**
- Row exists, `is_error=true`, real non-zero input tokens recorded.

**Fail:**
- No row is produced for the errored call, or the row shows $0/0-token despite the provider having consumed input — this is a confirmed regression against the #6574 fix and must be filed as a bug.
