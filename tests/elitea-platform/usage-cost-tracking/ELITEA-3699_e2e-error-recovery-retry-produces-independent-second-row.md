---
id: ELITEA-3699
title: "E2E: Build/Edit-with-AI error-then-retry journey records a real-input-token error row, then an independent, non-double-billed retry row"
priority: high
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, integration, e2e, error-handling]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3699: E2E: Build/Edit-with-AI error-then-retry journey records a real-input-token error row, then an independent, non-double-billed retry row

**Module:** usage-cost-tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a first Build-with-AI (or Edit-with-AI) attempt errors after the provider received input, a `usage_event` row is recorded with real input tokens and `is_error=true`; when the user then retries, a **second, independent** row is recorded — not merged with the first, and not double-billed via idempotency-key reuse.

---

## Preconditions

- Logged in to {{base_url}} with permission to create/edit agents.
- Ability to force a provider-side failure on the first attempt only (e.g. a transient misconfiguration corrected before the retry), so the retry can succeed.

---

## Test Data

| Field | Value |
|-------|-------|
| Description/request | Same natural-language input reused for both the failing attempt and the retry |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a Build-with-AI (or Edit-with-AI) call under a condition that causes the provider to accept input and then fail. | Call fails; UI surfaces the error. |
| 2 | Inspect `usage_event` for this attempt. | A row exists with `is_error=true` and real (non-zero) input token counts. |
| 3 | Correct the failure condition, then retry the identical request. | Second call succeeds (or fails again — either way, a new attempt is dispatched). |
| 4 | Inspect `usage_event` for the retry. | A **second, independent** row exists — distinct `id`/timestamp from the first row, with its own token counts. |
| 5 | Confirm the retry's cost was not suppressed or merged due to idempotency-key reuse from the first attempt. | Retry is billed on its own merits as a separate call; total cost reflects both attempts, not just one. |

---

## Expected Final State

Two independent `usage_event` rows exist for the error-then-retry sequence: one errored row with real input tokens, one retry row billed independently.

---

## Pass/Fail Criteria

**Pass:**
- First attempt's row has `is_error=true` with real input tokens.
- Retry produces a distinct second row, correctly billed on its own.

**Fail:**
- First attempt produces no row or a $0/0-token row despite the provider receiving input.
- Retry is merged into the first row or silently not billed due to idempotency-key reuse.
