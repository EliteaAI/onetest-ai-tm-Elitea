---
id: ELITEA-3689
title: "LLM timeout counts only tokens actually received; malformed/unparseable response still produces a row with token_source='unparsed'"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, error-handling, llm]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571"]
---

# ELITEA-3689: LLM timeout counts only tokens actually received; malformed/unparseable response still produces a row with token_source='unparsed'

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that a timed-out LLM call records only the tokens actually received (no "estimated" counts for incomplete responses), and that a malformed/unparseable provider response still produces a `usage_event` row with `token_source='unparsed'` (not a thrown error or a silently dropped row).

---

## Preconditions

- Logged in to {{base_url}}.
- Ability to force or reproduce a timeout and, separately, a malformed/unparseable provider response in the test environment (e.g. via a slow/misbehaving model endpoint, if available).

---

## Test Data

| Field | Value |
|-------|-------|
| Timeout trigger | Any reproducible slow/non-responding endpoint in the test environment |
| Malformed-response trigger | Any reproducible endpoint returning a non-standard/unparseable usage payload |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger an LLM call that times out. | Call fails with a timeout error in the UI. |
| 2 | Inspect the resulting `usage_event` row. | Only tokens actually received before the timeout are counted — no "estimated" token counts are fabricated for the incomplete response. |
| 3 | Trigger an LLM call against an endpoint that returns a malformed/unparseable usage payload. | Call completes (success or error) but the usage data in the response can't be parsed normally. |
| 4 | Inspect the resulting `usage_event` row. | A row is still produced (not dropped); `token_source='unparsed'`; no unhandled exception is thrown to the user. |

---

## Expected Final State

Timeouts record only real received tokens (no estimation); malformed responses still produce a row tagged `token_source='unparsed'` rather than disappearing.

---

## Pass/Fail Criteria

**Pass:**
- Timeout row has no fabricated/estimated token counts.
- Malformed-response row exists with `token_source='unparsed'`.

**Fail:**
- Timeout row shows estimated/guessed token counts.
- Malformed-response call throws an unhandled error or silently drops the row instead of recording `token_source='unparsed'`.
